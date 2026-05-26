---
description: What Is a Relayer?
---

# V. Voidify Relayers

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

***

## English

### What Is a Relayer?

A relayer submits a private withdrawal transaction on behalf of a user. The user generates the zero-knowledge proof, and the relayer broadcasts the transaction without gaining access to the user's deposited funds.

Relayers help users avoid broadcasting a withdrawal from their own wallet and can serve recipients that do not yet hold SOL for transaction fees.

### How It Works

1. A user generates a zero-knowledge withdrawal proof off-chain.
2. The user sends the withdrawal request to a relayer.
3. The relayer submits the transaction on-chain.
4. The recipient receives the withdrawn funds.
5. The relayer receives its configured fee.

### Become a Relayer

You need:

* A server with at least 2 GB RAM; Ubuntu is recommended.
* A domain pointed to the server, with ports `80` and `443` open.
* A unique relayer name, a public HTTPS service URL, a fee rate, and the required stake.

#### 1. Install Docker on Ubuntu

```bash
sudo apt update
sudo apt install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
```

#### 2. Download and Configure

```bash
git clone <VOIDIFY_RELAYER_DOCKER_GITHUB_URL> voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
The Docker repository link will be published here shortly.
{% endhint %}

Edit `.env` and set your domain and one relayer key option:

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

Or:

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

#### 3. Start

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy automatically serves HTTPS for the domain specified in `.env`.

#### 4. Register

Registration is live at [https://voidify.4sol.xyz](https://voidify.4sol.xyz).

Enter your relayer name, HTTPS endpoint, fee rate, and stake amount, then submit the transaction.

{% hint style="info" %}
Relayer SDK documentation is currently being updated.
{% endhint %}

### Fees and Management

* You receive your configured relayer fee for withdrawals you process.
* You can add stake, update your fee, and update your endpoint.
* If your stake drops below the active threshold, the relayer is deactivated until sufficient stake is added.
* Users can choose an active relayer in the application.

***

## 中文

### 什么是 Relayer？

Relayer 代表用户提交隐私提款交易。用户在链下生成零知识证明，relayer 负责广播交易，但无法访问用户的存款资金。

通过 relayer 提款，用户不需要使用自己的钱包广播提款交易；当收款地址还没有用于交易手续费的 SOL 时，也可以完成提款。

### 工作流程

1. 用户在链下生成零知识提款证明。
2. 用户将提款请求发送给 relayer。
3. Relayer 在链上提交交易。
4. 收款地址收到提款资金。
5. Relayer 收到其设置的手续费。

### 成为 Relayer

你需要准备：

* 一台至少 2 GB 内存的服务器，建议使用 Ubuntu。
* 一个解析到该服务器的域名，并开放端口 `80` 和 `443`。
* 唯一的 relayer 名称、公开的 HTTPS 服务地址、手续费率及所需质押。

#### 1. 在 Ubuntu 上安装 Docker

```bash
sudo apt update
sudo apt install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
```

#### 2. 下载并配置

```bash
git clone <VOIDIFY_RELAYER_DOCKER_GITHUB_URL> voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Docker 仓库链接将很快在此发布。
{% endhint %}

编辑 `.env`，设置域名和其中一种 relayer 密钥配置：

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

或：

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

#### 3. 启动

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy 会自动为 `.env` 中设置的域名提供 HTTPS。

#### 4. 注册

Relayer 注册现已开放：[https://voidify.4sol.xyz](https://voidify.4sol.xyz)。

填写 relayer 名称、HTTPS 服务地址、手续费率及质押金额，然后提交交易。

{% hint style="info" %}
Relayer SDK 文档正在更新中。
{% endhint %}

### 手续费与管理

* 对于处理的提款，你将获得所设置的 relayer 手续费。
* 你可以增加质押、更新手续费率和服务地址。
* 如果质押低于活跃阈值，relayer 将被停用，直到补充足够质押。
* 用户可以在应用中选择活跃的 relayer。

***

## Русский

### Что такое Relayer?

Relayer отправляет транзакцию приватного вывода от имени пользователя. Пользователь генерирует доказательство с нулевым разглашением вне сети, а relayer публикует транзакцию, не получая доступа к внесенным средствам пользователя.

Relayer позволяет пользователю не публиковать вывод из собственного кошелька и помогает получателю вывести средства, даже если у него еще нет SOL для комиссии транзакции.

### Как это работает

1. Пользователь создает доказательство приватного вывода вне сети.
2. Пользователь отправляет запрос на вывод relayer.
3. Relayer отправляет транзакцию в сеть.
4. Получатель получает выведенные средства.
5. Relayer получает установленную им комиссию.

### Как стать Relayer

Вам необходимы:

* Сервер с оперативной памятью не менее 2 GB; рекомендуется Ubuntu.
* Домен, направленный на сервер, с открытыми портами `80` и `443`.
* Уникальное имя relayer, публичный HTTPS-адрес сервиса, ставка комиссии и требуемый стейк.

#### 1. Установите Docker на Ubuntu

```bash
sudo apt update
sudo apt install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
```

#### 2. Загрузите и настройте

```bash
git clone <VOIDIFY_RELAYER_DOCKER_GITHUB_URL> voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Ссылка на Docker-репозиторий будет опубликована здесь в ближайшее время.
{% endhint %}

Измените `.env`, указав домен и один из вариантов ключа relayer:

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

Или:

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

#### 3. Запустите

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy автоматически включает HTTPS для домена, указанного в `.env`.

#### 4. Зарегистрируйтесь

Регистрация relayer уже доступна на [https://voidify.4sol.xyz](https://voidify.4sol.xyz).

Укажите имя relayer, HTTPS-адрес сервиса, ставку комиссии и сумму стейка, затем отправьте транзакцию.

{% hint style="info" %}
Документация Relayer SDK обновляется.
{% endhint %}

### Комиссии и управление

* За обработанные выводы вы получаете установленную вами комиссию relayer.
* Вы можете добавить стейк, изменить комиссию и обновить адрес сервиса.
* Если стейк становится ниже активного порога, relayer деактивируется до пополнения стейка.
* Пользователи могут выбрать активный relayer в приложении.

***

## 日本語

### Relayer とは

Relayer は、ユーザーに代わってプライベート出金トランザクションを送信します。ユーザーがオフチェーンでゼロ知識証明を生成し、relayer はユーザーの預入資金にアクセスすることなくトランザクションをブロードキャストします。

Relayer を利用すると、ユーザー自身のウォレットから出金トランザクションを送信する必要がありません。また、受取アドレスが取引手数料用の SOL をまだ持っていない場合にも対応できます。

### 動作の流れ

1. ユーザーがオフチェーンでゼロ知識出金証明を生成します。
2. ユーザーが出金リクエストを relayer に送信します。
3. Relayer がオンチェーンでトランザクションを送信します。
4. 受取アドレスが出金された資金を受け取ります。
5. Relayer が設定した手数料を受け取ります。

### Relayer になる

必要なもの：

* 2 GB 以上のメモリを持つサーバー。Ubuntu を推奨します。
* サーバーを指すドメインと、開放されたポート `80` および `443`。
* 一意の relayer 名、公開 HTTPS サービス URL、手数料率、必要なステーク。

#### 1. Ubuntu に Docker をインストール

```bash
sudo apt update
sudo apt install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
sudo tee /etc/apt/sources.list.d/docker.sources > /dev/null <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
```

#### 2. ダウンロードして設定

```bash
git clone <VOIDIFY_RELAYER_DOCKER_GITHUB_URL> voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Docker リポジトリのリンクは近日中にここで公開します。
{% endhint %}

`.env` を編集し、ドメインといずれかの relayer キー設定を入力します。

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

または：

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

#### 3. 起動

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy は `.env` で指定されたドメインに対して HTTPS を自動的に提供します。

#### 4. 登録

Relayer の登録は [https://voidify.4sol.xyz](https://voidify.4sol.xyz) で利用できます。

Relayer 名、HTTPS サービス URL、手数料率、ステーク量を入力し、登録トランザクションを送信します。

{% hint style="info" %}
Relayer SDK のドキュメントは現在更新中です。
{% endhint %}

### 手数料と管理

* 処理した出金について、設定した relayer 手数料を受け取ります。
* ステークの追加、手数料率の変更、サービス URL の更新ができます。
* ステークが有効化のしきい値を下回ると、十分なステークを追加するまで relayer は無効化されます。
* ユーザーはアプリケーションで有効な relayer を選択できます。
