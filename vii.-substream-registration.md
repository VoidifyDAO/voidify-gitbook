# VII. Substream Registration


***

## English

A Voidify Substream peer indexes public protocol events and serves them to clients over HTTP. In `peer` mode, clients discover available peers from on-chain `SubstreamConfig` accounts instead of relying on a hard-coded server list.

An on-chain registration publishes the operator's Solana public key (`owner`) and the peer's public base URL (`url`). It is a discovery and identity mechanism; it does not grant custody of funds or permission to change protocol state.

### Requirements

Before operating a registered peer, prepare:

* a server with a current Node.js LTS release, persistent storage, and a reliable Solana RPC connection
* a domain pointing to the server, with inbound ports `80` and `443` reachable
* a dedicated Solana keypair for the service, with enough SOL for maintenance transactions
* the Voidify program ID for the selected network

The same keypair must run the service and be recorded as `owner`. Clients challenge `/api/identity` and verify that its response is signed by the registered owner.

The registered URL must be a valid `http://` or `https://` base URL, point to the service root rather than `/api` or `/health`, and be no longer than **128 UTF-8 bytes**. Public nodes should use their final HTTPS URL, for example `https://substream.example.com`.

### 1. Install and Configure the CLI

The commands below target Voidify CLI v3.1.1. Confirm that the installed build exposes the service command:

```bash
npm install -g @voidifydao/sdk@3.1.1
voidify substream start --help
```

Create a dedicated configuration:

```bash
CONFIG="$HOME/.config/voidify/substream.json"

voidify config init --type substream --path "$CONFIG"
voidify -c "$CONFIG" config set rpcUrl "https://YOUR_SOLANA_RPC"
voidify -c "$CONFIG" config set programId "4WJnXP7mFxFY45SYvfyGDwEBdcwafVqdgbYYSHpoded4"
voidify -c "$CONFIG" config set keypair.path "/secure/path/operator-wallet.json"
voidify -c "$CONFIG" config set substreamServer.host "127.0.0.1"
voidify -c "$CONFIG" config set substreamServer.port 3003
voidify -c "$CONFIG" config set substreamServer.dbPath "/var/lib/voidify/substream.db"
```

Keep the wallet file outside the web root, restrict its filesystem permissions, and never publish its contents. Preserve the SQLite database across restarts and deployments.

### 2. Start the Service

```bash
voidify -c "$CONFIG" substream start
```

The service listens on `127.0.0.1:3003` so only the reverse proxy can reach it. Use a process supervisor so it restarts after a crash or server reboot.

Check the backend locally before configuring the proxy:

```bash
curl "http://127.0.0.1:3003/health"
```

### 3. Configure the Reverse Proxy with Caddy

#### Point the Domain to the Server

Create a DNS `A` record for `substream.example.com` pointing to the server's public IPv4 address. Add an `AAAA` record only if IPv6 is correctly configured. Allow inbound TCP `80` and `443` through the cloud security group, NAT, and host firewall, then wait until the domain resolves to this server.

#### Install Caddy

On Ubuntu or Debian:

```bash
sudo apt update
sudo apt install -y caddy
sudo systemctl enable --now caddy
```

If the distribution does not provide the `caddy` package, use the official [Caddy installation instructions](https://caddyserver.com/docs/install#debian-ubuntu-raspbian).

#### Add the Site Configuration

Open the Caddy configuration:

```bash
sudoedit /etc/caddy/Caddyfile
```

Add this site block. If the file already contains other sites, keep them and append this block:

```caddyfile
substream.example.com {
    encode zstd gzip
    reverse_proxy 127.0.0.1:3003
}
```

Caddy preserves the path and query string by default, including the `audience` and `nonce` parameters used by `/api/identity`. When DNS and ports `80`/`443` are ready, Caddy automatically obtains and renews the TLS certificate.

#### Validate and Reload

```bash
sudo caddy validate --config /etc/caddy/Caddyfile --adapter caddyfile
sudo systemctl reload caddy
sudo systemctl status caddy --no-pager
```

If UFW is enabled, allow the public web ports:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Do not expose port `3003` to the internet when Caddy runs on the same server. This upstream address assumes a native same-host deployment; if Caddy runs in a container, use the Substream service name on a shared container network instead of `127.0.0.1`.

#### Verify the Public URL

```bash
curl -I "http://substream.example.com/health"
curl -fsS "https://substream.example.com/health"
curl -fsS "https://substream.example.com/api/scopes"

BASE_URL="https://substream.example.com"
curl -fsS --get "$BASE_URL/api/identity" \
  --data-urlencode "audience=$BASE_URL" \
  --data-urlencode "nonce=registration-check"
```

The HTTP request should redirect to HTTPS. The health response should report `ok` after startup or synchronization, and the identity response's `owner` must equal the public key you plan to register. Repeat the checks from another device or network to cover cloud firewall and NAT rules. Keep the server clock synchronized: identity timestamps are accepted within approximately 60 seconds.

{% hint style="info" %}
A healthy new peer may initially return an empty scope list. It can discover scopes from chain data or other registered peers as traffic and synchronization begin.
{% endhint %}

{% hint style="warning" %}
`502 Bad Gateway` means Caddy cannot reach `127.0.0.1:3003`. Check `curl http://127.0.0.1:3003/health`, the configured host/port, and `sudo journalctl -u caddy -n 100 --no-pager`. Certificate failures usually mean DNS is wrong, ports `80`/`443` are blocked, or another service already occupies those ports.
{% endhint %}

### 4. Verify the Registration

After the owner and URL have been added to the on-chain registry, verify the record:

```bash
voidify -c "$CONFIG" substream list "<SUBSTREAM_OWNER_PUBKEY>"
```

Confirm that the returned owner and URL exactly match the running service. A client using `peer` mode can then discover the account, challenge the identity endpoint, and use the peer if identity and health checks succeed.

### Updating a Registration

The registered owner can update the URL directly:

```bash
voidify -c "$CONFIG" substream update \
  --url "https://new-substream.example.com"
```

Bring the new endpoint online with the **same owner keypair** before updating the chain record. The owner cannot be changed through the URL update command.

### Operator Checklist

* Register the final HTTPS URL, with no `/api` suffix
* Keep DNS, TLS, the reverse proxy, and the system clock healthy
* Keep `/health`, `/api/identity`, `/api/scopes`, and event endpoints publicly reachable
* Run the service with the same keypair as the registered owner
* Protect the wallet file and keep enough SOL for maintenance transactions
* Preserve the SQLite database and monitor synchronization errors
* Verify the chain record after every URL update

***

## 中文

Voidify Substream peer 会索引协议的公开链上事件，并通过 HTTP 提供给客户端。在 `peer` 模式下，客户端从链上的 `SubstreamConfig` 账户发现可用节点，而不是依赖写死的服务器列表。

链上注册记录发布运营者的 Solana 公钥（`owner`）和节点的公开基础 URL（`url`）。注册只用于节点发现和身份验证，不会赋予运营者资金托管权或协议状态修改权。

### 准备条件

运行已注册节点前，请准备：

* 一台安装当前 Node.js LTS、具备持久化存储并能稳定连接 Solana RPC 的服务器
* 一个指向服务器的域名，并确保公网可以访问 `80` 和 `443` 端口
* 一个专用于 Substream 服务的 Solana keypair，并预留足够 SOL 支付维护交易
* 所选网络的 Voidify program ID

运行服务的 keypair 必须与链上记录的 `owner` 完全一致。客户端会请求 `/api/identity`，并验证响应是否由已注册 owner 签名。

注册 URL 必须是有效的 `http://` 或 `https://` 基础 URL，指向服务根地址而不是 `/api` 或 `/health`，并且不超过 **128 个 UTF-8 字节**。公开节点应注册最终 HTTPS 地址，例如 `https://substream.example.com`。

### 1. 安装并配置 CLI

下面的命令以 Voidify CLI v3.1.1 为准。安装后先确认该构建包含服务启动命令：

```bash
npm install -g @voidifydao/sdk@3.1.1
voidify substream start --help
```

创建独立配置：

```bash
CONFIG="$HOME/.config/voidify/substream.json"

voidify config init --type substream --path "$CONFIG"
voidify -c "$CONFIG" config set rpcUrl "https://YOUR_SOLANA_RPC"
voidify -c "$CONFIG" config set programId "4WJnXP7mFxFY45SYvfyGDwEBdcwafVqdgbYYSHpoded4"
voidify -c "$CONFIG" config set keypair.path "/secure/path/operator-wallet.json"
voidify -c "$CONFIG" config set substreamServer.host "127.0.0.1"
voidify -c "$CONFIG" config set substreamServer.port 3003
voidify -c "$CONFIG" config set substreamServer.dbPath "/var/lib/voidify/substream.db"
```

钱包文件应放在 Web 根目录之外，并设置严格的文件权限，绝不要公开其内容。SQLite 数据库需要在重启和部署更新之间持久保存。

### 2. 启动服务

```bash
voidify -c "$CONFIG" substream start
```

服务监听 `127.0.0.1:3003`，只有同一服务器上的反向代理可以访问。建议使用进程守护工具，让服务在崩溃或服务器重启后自动恢复。

配置反向代理前，先在服务器本机检查后端：

```bash
curl "http://127.0.0.1:3003/health"
```

### 3. 使用 Caddy 配置反向代理

#### 将域名指向服务器

为 `substream.example.com` 创建 DNS `A` 记录，指向服务器的公网 IPv4 地址。只有在 IPv6 已正确配置时才添加 `AAAA` 记录。在云安全组、NAT 和主机防火墙中放行入站 TCP `80` 与 `443`，并确认域名已经解析到这台服务器。

#### 安装 Caddy

在 Ubuntu 或 Debian 上运行：

```bash
sudo apt update
sudo apt install -y caddy
sudo systemctl enable --now caddy
```

如果系统软件源没有 `caddy` 软件包，请按照 [Caddy 官方安装说明](https://caddyserver.com/docs/install#debian-ubuntu-raspbian)安装。

#### 添加站点配置

打开 Caddy 配置文件：

```bash
sudoedit /etc/caddy/Caddyfile
```

添加以下站点配置。如果文件中已有其他站点，请保留原内容并追加此配置块：

```caddyfile
substream.example.com {
    encode zstd gzip
    reverse_proxy 127.0.0.1:3003
}
```

Caddy 默认会完整转发请求路径和查询参数，包括 `/api/identity` 使用的 `audience` 和 `nonce`。DNS 和 `80`/`443` 端口准备完成后，Caddy 会自动申请并续期 TLS 证书。

#### 验证并重新加载

```bash
sudo caddy validate --config /etc/caddy/Caddyfile --adapter caddyfile
sudo systemctl reload caddy
sudo systemctl status caddy --no-pager
```

如果启用了 UFW，请放行公网 Web 端口：

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Caddy 与 Substream 原生运行在同一台服务器时，不要将 `3003` 端口开放到公网。如果 Caddy 运行在容器中，容器内的 `127.0.0.1` 指向 Caddy 自身，应改为同一容器网络中的 Substream 服务名。

#### 验证公开地址

```bash
curl -I "http://substream.example.com/health"
curl -fsS "https://substream.example.com/health"
curl -fsS "https://substream.example.com/api/scopes"

BASE_URL="https://substream.example.com"
curl -fsS --get "$BASE_URL/api/identity" \
  --data-urlencode "audience=$BASE_URL" \
  --data-urlencode "nonce=registration-check"
```

HTTP 请求应重定向到 HTTPS。启动或同步完成后，health 响应应显示 `ok`，identity 响应中的 `owner` 必须等于计划注册的公钥。最好再从另一台设备或另一网络测试一次，以覆盖云防火墙和 NAT。服务器系统时间也必须保持同步，因为 identity 时间戳允许的误差约为 60 秒。

{% hint style="info" %}
一个刚启动且健康的新节点可能暂时返回空的 scope 列表。随着请求和同步开始，它可以从链上数据或其他已注册 peer 发现 scope。
{% endhint %}

{% hint style="warning" %}
出现 `502 Bad Gateway` 表示 Caddy 无法连接 `127.0.0.1:3003`。请检查 `curl http://127.0.0.1:3003/health`、监听地址和端口，并查看 `sudo journalctl -u caddy -n 100 --no-pager`。证书申请失败通常是 DNS 配置错误、`80`/`443` 被拦截，或其他服务已经占用这些端口。
{% endhint %}

### 4. 验证链上注册

owner 和 URL 被写入链上注册表后，使用以下命令核对记录：

```bash
voidify -c "$CONFIG" substream list "<SUBSTREAM_OWNER_PUBKEY>"
```

确认返回的 owner 和 URL 与正在运行的服务完全一致。使用 `peer` 模式的客户端随后会发现该账户、验证 identity endpoint，并在身份与健康检查通过后使用该节点。

### 更新注册

已注册 owner 可以直接更新 URL：

```bash
voidify -c "$CONFIG" substream update \
  --url "https://new-substream.example.com"
```

更新链上记录前，应先让新地址使用**同一个 owner keypair**正常上线。URL 更新命令不能修改 owner。

### 运营检查清单

* 注册最终 HTTPS URL，不要添加 `/api` 后缀
* 保持 DNS、TLS、反向代理和系统时间正常
* 保证 `/health`、`/api/identity`、`/api/scopes` 和事件端点可公开访问
* 使用与链上 owner 相同的 keypair 运行服务
* 保护钱包文件，并保留足够 SOL 用于维护交易
* 持久保存 SQLite 数据库并监控同步错误
* 每次更新 URL 后重新核对链上记录

***

## Русский

Voidify Substream peer индексирует публичные события протокола и предоставляет их клиентам по HTTP. В режиме `peer` клиенты находят узлы через ончейн-аккаунты `SubstreamConfig`, а не через жестко заданный список серверов.

Регистрация публикует публичный ключ оператора (`owner`) и базовый URL узла (`url`). Она используется для обнаружения и проверки identity, но не дает оператору доступ к средствам или право изменять protocol state.

### Требования

Подготовьте server с актуальной Node.js LTS, persistent storage и надежным Solana RPC; domain, направленный на server, с доступными портами `80` и `443`; отдельный Solana keypair с SOL; Voidify program ID.

Service keypair должен совпадать с зарегистрированным `owner`. Клиенты проверяют его подпись через `/api/identity`. URL должен быть корректным базовым `http://` или `https://` адресом, указывать на корень сервиса без `/api` и не превышать **128 байт UTF-8**. Для public node используйте окончательный HTTPS URL.

### 1. Установите и настройте CLI

Команды ниже рассчитаны на Voidify CLI v3.1.1:

```bash
npm install -g @voidifydao/sdk@3.1.1
voidify substream start --help

CONFIG="$HOME/.config/voidify/substream.json"
voidify config init --type substream --path "$CONFIG"
voidify -c "$CONFIG" config set rpcUrl "https://YOUR_SOLANA_RPC"
voidify -c "$CONFIG" config set programId "4WJnXP7mFxFY45SYvfyGDwEBdcwafVqdgbYYSHpoded4"
voidify -c "$CONFIG" config set keypair.path "/secure/path/operator-wallet.json"
voidify -c "$CONFIG" config set substreamServer.host "127.0.0.1"
voidify -c "$CONFIG" config set substreamServer.port 3003
voidify -c "$CONFIG" config set substreamServer.dbPath "/var/lib/voidify/substream.db"
```

Храните wallet-файл вне web root, ограничьте права доступа и сохраняйте SQLite-базу между обновлениями.

### 2. Запустите сервис

```bash
voidify -c "$CONFIG" substream start
```

Service слушает `127.0.0.1:3003`, поэтому напрямую доступен только reverse proxy на том же server. Используйте process supervisor для автоматического перезапуска.

```bash
curl "http://127.0.0.1:3003/health"
```

### 3. Настройте Reverse Proxy через Caddy

#### Направьте домен на Server

Создайте DNS `A` record для `substream.example.com`, направленный на public IPv4 server. Добавляйте `AAAA` только при рабочем IPv6. В cloud security group, NAT и host firewall разрешите входящий TCP на `80` и `443`.

#### Установите Caddy

Установите Caddy:

```bash
sudo apt update
sudo apt install -y caddy
sudo systemctl enable --now caddy
```

Если package отсутствует, используйте официальную [инструкцию по установке Caddy](https://caddyserver.com/docs/install#debian-ubuntu-raspbian).

#### Добавьте конфигурацию сайта

Откройте config:

```bash
sudoedit /etc/caddy/Caddyfile
```

Добавьте site block, сохранив другие существующие сайты:

```caddyfile
substream.example.com {
    encode zstd gzip
    reverse_proxy 127.0.0.1:3003
}
```

Caddy сохраняет path и query string, поэтому параметры `audience` и `nonce` не требуют отдельных правил. После готовности DNS и портов Caddy автоматически получает и продлевает TLS certificate.

#### Проверьте и перезагрузите

```bash
sudo caddy validate --config /etc/caddy/Caddyfile --adapter caddyfile
sudo systemctl reload caddy
sudo systemctl status caddy --no-pager
```

Если используется UFW:

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

#### Проверьте Public URL

Не открывайте port `3003` в internet. Этот upstream подходит для native same-host deployment; если Caddy работает в container, используйте имя Substream service в общей container network вместо `127.0.0.1`. Проверьте public URL, желательно также с другого устройства или сети:

```bash
curl -I "http://substream.example.com/health"
curl -fsS "https://substream.example.com/health"
curl -fsS "https://substream.example.com/api/scopes"

BASE_URL="https://substream.example.com"
curl -fsS --get "$BASE_URL/api/identity" \
  --data-urlencode "audience=$BASE_URL" \
  --data-urlencode "nonce=registration-check"
```

HTTP request должен перенаправляться на HTTPS. Health должен вернуть `ok`, а `owner` в identity response — совпасть с регистрируемым ключом. Синхронизируйте часы server: допустимая погрешность timestamp составляет около 60 секунд.

{% hint style="info" %}
Новый healthy peer сначала может вернуть пустой список scopes. Он обнаружит scopes из chain data или у других зарегистрированных peers по мере начала requests и synchronization.
{% endhint %}

{% hint style="warning" %}
При `502 Bad Gateway` сначала проверьте `curl http://127.0.0.1:3003/health`, затем Caddyfile и `sudo journalctl -u caddy -n 100 --no-pager`. Ошибки TLS обычно вызваны неверными A/AAAA records, закрытыми портами `80`/`443` или другим service, уже занявшим эти порты.
{% endhint %}

### 4. Проверьте и обновите запись

После добавления owner и URL в ончейн-реестр проверьте запись:

```bash
voidify -c "$CONFIG" substream list "<SUBSTREAM_OWNER_PUBKEY>"

voidify -c "$CONFIG" substream update \
  --url "https://new-substream.example.com"
```

Новый endpoint должен заранее работать с **тем же owner keypair**. Команда обновления URL не может изменить owner.

Следите за DNS, TLS, reverse proxy, системными часами, публичной доступностью `/health`, `/api/identity`, `/api/scopes` и event endpoints. Защищайте wallet-файл, сохраняйте database и проверяйте ончейн-запись после каждого изменения.

***

## 日本語

Voidify Substream peer は protocol の公開 on-chain event を index し、HTTP 経由で client に提供します。`peer` mode の client は、固定 server list ではなく on-chain の `SubstreamConfig` account から peer を発見します。

Registration が公開するのは operator public key（`owner`）と public base URL（`url`）です。これは discovery と identity verification の仕組みであり、operator に資金 custody や protocol state の変更権限を与えません。

### 要件

現行 Node.js LTS、persistent storage、安定した Solana RPC を備えた server、server を向いた domain と到達可能な `80`/`443` ports、専用 Solana keypair と SOL、対象 network の Voidify program ID を準備します。

Service keypair は登録する `owner` と同一でなければなりません。Client は `/api/identity` の署名を検証します。URL は有効な `http://` または `https://` base URL で、`/api` を付けず、**128 UTF-8 bytes** 以下にします。Public node は最終 HTTPS URL を使用してください。

### 1. CLI のインストールと設定

以下は Voidify CLI v3.1.1 向けです。

```bash
npm install -g @voidifydao/sdk@3.1.1
voidify substream start --help

CONFIG="$HOME/.config/voidify/substream.json"
voidify config init --type substream --path "$CONFIG"
voidify -c "$CONFIG" config set rpcUrl "https://YOUR_SOLANA_RPC"
voidify -c "$CONFIG" config set programId "4WJnXP7mFxFY45SYvfyGDwEBdcwafVqdgbYYSHpoded4"
voidify -c "$CONFIG" config set keypair.path "/secure/path/operator-wallet.json"
voidify -c "$CONFIG" config set substreamServer.host "127.0.0.1"
voidify -c "$CONFIG" config set substreamServer.port 3003
voidify -c "$CONFIG" config set substreamServer.dbPath "/var/lib/voidify/substream.db"
```

Wallet file は web root の外に置き、permission を制限してください。SQLite database は restart や update をまたいで保持します。

### 2. Service の起動

```bash
voidify -c "$CONFIG" substream start
```

Service は `127.0.0.1:3003` を listen し、同じ server 上の reverse proxy だけが直接 access できます。Process supervisor で自動再起動も設定してください。

```bash
curl "http://127.0.0.1:3003/health"
```

### 3. Caddy Reverse Proxy の設定

#### Domain を Server に向ける

`substream.example.com` の DNS `A` record を server の public IPv4 に向けます。IPv6 が正しく動作する場合だけ `AAAA` record を追加してください。Cloud security group、NAT、host firewall で inbound TCP `80` と `443` を許可します。

#### Caddy のインストール

Caddy をインストールします。

```bash
sudo apt update
sudo apt install -y caddy
sudo systemctl enable --now caddy
```

Package がない場合は公式の [Caddy installation guide](https://caddyserver.com/docs/install#debian-ubuntu-raspbian) を使用してください。

#### Site Configuration の追加

Config を開きます。

```bash
sudoedit /etc/caddy/Caddyfile
```

既存 site がある場合は残したまま、次の block を追加します。

```caddyfile
substream.example.com {
    encode zstd gzip
    reverse_proxy 127.0.0.1:3003
}
```

Caddy は path と query string をそのまま転送するため、`audience` と `nonce` 用の追加 rule は不要です。DNS と ports が準備できると、TLS certificate を自動取得・更新します。

#### Validation と Reload

```bash
sudo caddy validate --config /etc/caddy/Caddyfile --adapter caddyfile
sudo systemctl reload caddy
sudo systemctl status caddy --no-pager
```

UFW を使用している場合：

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

#### Public URL の確認

Port `3003` は internet に公開しないでください。この upstream は native same-host deployment 用です。Caddy が container 内で動く場合は、`127.0.0.1` ではなく shared container network 上の Substream service name を使用します。可能であれば別の device または network から public URL も確認します。

```bash
curl -I "http://substream.example.com/health"
curl -fsS "https://substream.example.com/health"
curl -fsS "https://substream.example.com/api/scopes"

BASE_URL="https://substream.example.com"
curl -fsS --get "$BASE_URL/api/identity" \
  --data-urlencode "audience=$BASE_URL" \
  --data-urlencode "nonce=registration-check"
```

HTTP request は HTTPS に redirect され、health は `ok` を返す必要があります。Identity response の `owner` は登録予定 key と一致しなければなりません。Timestamp の許容差は約 60 秒なので server clock を同期してください。

{% hint style="info" %}
新しい healthy peer は、最初は空の scope list を返す場合があります。Requests と synchronization が始まると、chain data または他の registered peers から scopes を発見できます。
{% endhint %}

{% hint style="warning" %}
`502 Bad Gateway` の場合は、最初に `curl http://127.0.0.1:3003/health`、次に Caddyfile と `sudo journalctl -u caddy -n 100 --no-pager` を確認します。TLS error は、誤った A/AAAA records、閉じた `80`/`443` ports、または他 service による port 使用が主な原因です。
{% endhint %}

### 4. 確認・更新

Owner と URL が on-chain registry に追加された後、record を確認します。

```bash
voidify -c "$CONFIG" substream list "<SUBSTREAM_OWNER_PUBKEY>"

voidify -c "$CONFIG" substream update \
  --url "https://new-substream.example.com"
```

新 endpoint は、chain record の更新前に**同じ owner keypair**で起動してください。URL update command では owner を変更できません。

DNS、TLS、reverse proxy、system clock、`/health`、`/api/identity`、`/api/scopes`、event endpoints を監視してください。Wallet file と database を保護し、URL update のたびに on-chain record を確認します。
