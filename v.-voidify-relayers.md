---
description: What Is a Relayer?
---

# V. Voidify Relayers

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

***

## English

Relayers are independent participants within the Voidify protocol who help facilitate privacy-preserving withdrawals. By submitting transactions to the blockchain on behalf of users, relayers prevent withdrawal wallets from being linked to deposit addresses — all without ever accessing user funds or identities.

**Key Functions and Guarantees**

* **Privacy-Preserving**: Allows users to withdraw without revealing their own wallet address on-chain
* **Trustless Operation**: Relayers cannot alter, reroute, or access deposited funds — all transaction data is validated by zero-knowledge proofs
* **Gas Support**: Useful when the recipient wallet has no SOL to cover transaction fees
* **Decentralized Network**: The relayer system is open and community-run; protocol developers have no centralized control

{% hint style="info" %}
Relayers are essential to Voidify’s privacy model — acting as anonymous broadcasters to maintain unlinkability between deposit and withdrawal events.
{% endhint %}

**Why Relayers Matter**

Even with zero-knowledge proofs, withdrawing directly from your own wallet exposes your public key on-chain. This reintroduces traceability and erodes privacy.

Relayers solve this by submitting your withdrawal transaction through their own address — unlinking you from both the proof and the transaction broadcast.

### ⚙️ How It Works

1. The user generates a zero-knowledge withdrawal proof off-chain
2. The user transmits the proof and request to a relayer via a private channel
3. The relayer broadcasts the transaction from their own address
4. Funds are transferred to the recipient address
5. The relayer receives a protocol-defined fee included in the transaction

Throughout this process, the relayer never knows the origin, identity, or intent of the user — preserving full operational privacy.

### 🚀 Becoming a Relayer

#### Requirements

To register as a relayer, you must:

* **Stake ∅ tokens**: A minimum stake amount is required for the first time(configurable by DAO, typically 10M ∅ tokens)
* **Provide a unique name**: 3–32 characters, lowercase alphanumeric + hyphen/underscore
* **Provide a service URL**: Your relayer endpoint where users can submit withdrawal requests
* **Set your fee rate**: Choose your relayer fee (max 10%)
* **Server** (2 GB of memory is enough)
* **Stay active**: minimum threshold(configurable by DAO, typically 1M ∅ tokens)

#### Registration Process

##### **1. Prepare a Server**

Get a VPS or dedicated server with at least 2 GB RAM. Any Linux distribution works (Ubuntu recommended).

##### **2. Point a Domain to Your Server**

Add a DNS **A record** pointing your domain (e.g. `relayer.example.com`) to your server's public IP address:

| Type | Name | Value |
| --- | --- | --- |
| A | relayer | `YOUR_SERVER_IP` |

Wait for DNS propagation (usually a few minutes, up to 24 hours).

##### **3. Install Docker on Ubuntu**

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

##### **4. Download and Configure the Relayer**

Clone the Docker deployment repository:

```bash
git clone https://github.com/VoidifyCommunity/voidify-relayer.git voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Docker deployment repository: [https://github.com/VoidifyCommunity/voidify-relayer](https://github.com/VoidifyCommunity/voidify-relayer)
{% endhint %}

Edit `.env` and set your domain and one relayer key option:

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

Or use a keypair JSON file instead:

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

##### **5. Run the Relayer**

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy automatically serves HTTPS for the domain specified in `.env`.

##### **6. Register On-Chain**

Once your relayer service is running and accessible via HTTPS, register on-chain on frontend(voidify.4sol.xyz)\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

Registration is live at [https://voidify.4sol.xyz](https://voidify.4sol.xyz).

Enter your relayer name, HTTPS endpoint, fee rate, and stake amount, then submit the transaction.

### What You Earn

As a registered relayer, you earn:

* **Relayer Fee**: Your custom fee rate (up to 10%) on every withdrawal you process
* **Platform Fee (in SOL)**: You receive the platform's fee portion in SOL upfront
* **Token Deduction**: The platform fee's token equivalent is deducted from your staked ∅ tokens and sent to the DAO treasury

> **Example**: If you process a 10 SOL withdrawal with a 0.1% relayer fee and 0.3% DAO fee:
>
> * You receive: 0.01 SOL (relayer fee) + 0.03 SOL (DAO fee) = **0.04 SOL**
> * Your stake is reduced by: 0.03 SOL worth of ∅ tokens (based on oracle price)
> * User receives: 9.96 SOL

### 🎯 Relayer Selection Mechanism

Voidify implements an intelligent, weighted random selection algorithm to automatically choose the optimal relayer for each withdrawal transaction. This ensures a balance between cost-efficiency, reliability, and decentralization.

#### How Relayers Are Selected

When a user initiates a withdrawal, the system:

1. **Filters Active Relayers**: Only considers relayers that are:
   * Registered and active on-chain
   * Passing health checks (responsive API endpoints)
   * Above the minimum stake threshold
2.  **Calculates Selection Weight**: Each relayer receives a score based on:

    ```txt
    Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
    ```

    This formula means:

    * **Higher stake** = Higher selection probability (more skin in the game)
    * **Lower fees** = Higher selection probability (better for users)
    * The fee penalty is quadratic, so high-fee relayers are strongly discouraged
3. **Weighted Random Selection**: Relayers are chosen probabilistically based on their scores
   * A relayer with 2x the score has 2x the chance of being selected
   * This prevents monopolization while rewarding quality service

#### Selection Examples

**Example 1: Two Relayers**

* Relayer A: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B: 5M ∅ stake, 50 bps (0.5%) fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

Selection probability:

* Relayer A: 61.5% chance
* Relayer B: 38.5% chance

**Example 2: Low Fee Advantage**

* Relayer A: 10M ∅ stake, 10 bps (0.1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × 0.75 = 7,500,000

Selection probability:

* Relayer A: 57% chance (significantly rewarded for lower fee)
* Relayer C: 43% chance

#### Benefits of This Approach

✅ **Fair Competition**: New relayers with competitive fees can gain market share&#x20;

✅ **Quality Incentive**: Higher stakes and lower fees are rewarded with more business&#x20;

✅ **Decentralization**: Prevents any single relayer from dominating the network&#x20;

✅ **User Protection**: Automatically favors cost-effective, well-capitalized relayers

✅ **Transparency**: Selection algorithm is open-source and verifiable

#### Manual Selection

Users can also manually choose a specific relayer from the interface if they prefer:

* View all active relayers with their fees
* Sort by fee (lowest first) or stake (highest first)
* Select any relayer for their withdrawal

This gives users full control while providing intelligent defaults for convenience.

### Relayer Management

Once registered, you can:

* **Add Stake**: Increase your staked ∅ tokens at any time
* **Update Fee**: Change your relayer fee rate (max 10%)
* **Update URL**: Change your service endpoint
* **Monitor Stats**: Track your total withdrawals processed, SOL earned, and tokens deducted

### Deactivation & Reactivation

* If your stake drops below the minimum threshold(default 1M) (due to DAO fee deductions), you are **automatically deactivated**
* You can reactivate by adding more ∅ tokens to bring your stake above the minimum
* Deactivated relayers cannot process new withdrawals until reactivated

### Unregistration

The DAO authority can:

* **Unregister** a relayer: Returns all staked tokens and removes the relayer from the network

***

## 中文

Relayer 是 Voidify 协议中的独立参与者，帮助用户完成保护隐私的提款。Relayer 代表用户把交易提交到链上，从而避免提款钱包和存款地址被关联，同时不会访问用户资金或身份。

**核心功能与保证**

* **保护隐私**：用户提款时无需暴露自己的链上钱包地址
* **无需信任**：Relayer 不能修改、重定向或访问存款资金，所有交易数据都由零知识证明验证
* **Gas 支持**：当收款钱包没有 SOL 支付交易手续费时尤其有用
* **去中心化网络**：Relayer 系统开放并由社区运行，协议开发者没有中心化控制权

{% hint style="info" %}
Relayer 是 Voidify 隐私模型的重要组成部分：它作为匿名广播者，维持存款事件与提款事件之间的不可关联性。
{% endhint %}

**为什么 Relayer 重要**

即使使用零知识证明，如果直接从自己的钱包提款，也会在链上暴露你的公钥。这会重新引入可追踪性并削弱隐私。

Relayer 通过自己的地址提交你的提款交易，将你与证明和交易广播过程都解除关联。

### ⚙️ 工作流程

1. 用户在链下生成零知识提款证明
2. 用户通过私密通道将证明和请求发送给 relayer
3. Relayer 使用自己的地址广播交易
4. 资金转入收款地址
5. Relayer 收到交易中包含的协议定义手续费

在整个过程中，relayer 不知道用户的来源、身份或意图，从而保持完整的操作隐私。

### 🚀 成为 Relayer

#### 要求

注册为 relayer 需要：

* **质押 ∅ 代币**：首次需要最低质押数量（由 DAO 配置，通常为 1000 万枚 ∅）
* **提供唯一名称**：3–32 个字符，小写字母数字及连字符/下划线
* **提供服务 URL**：用户提交提款请求的 relayer endpoint
* **设置手续费率**：选择你的 relayer fee（最高 10%）
* **服务器**：2 GB 内存即可
* **保持活跃**：最低活跃阈值（由 DAO 配置，通常为 100 万枚 ∅）

#### 注册流程

##### **1. 准备服务器**

准备一台至少 2 GB 内存的 VPS 或独立服务器。任意 Linux 发行版都可以，推荐 Ubuntu。

##### **2. 将域名指向服务器**

添加 DNS **A 记录**，将你的域名（例如 `relayer.example.com`）指向服务器公网 IP：

| 类型 | 名称 | 值 |
| --- | --- | --- |
| A | relayer | `YOUR_SERVER_IP` |

等待 DNS 生效，通常几分钟，最长可能 24 小时。

##### **3. 在 Ubuntu 上安装 Docker**

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

##### **4. 下载并配置 Relayer**

克隆 Docker 部署仓库：

```bash
git clone https://github.com/VoidifyCommunity/voidify-relayer.git voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Docker 部署仓库：[https://github.com/VoidifyCommunity/voidify-relayer](https://github.com/VoidifyCommunity/voidify-relayer)
{% endhint %}

编辑 `.env`，设置域名和其中一种 relayer 密钥配置：

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

或者使用密钥对 JSON 文件：

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

##### **5. 运行 Relayer**

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy 会自动为 `.env` 中设置的域名提供 HTTPS。

##### **6. 链上注册**

当 relayer 服务运行并可通过 HTTPS 访问后，在前端（voidify.4sol.xyz）进行链上注册。\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

Relayer 注册现已开放：[https://voidify.4sol.xyz](https://voidify.4sol.xyz)。

填写 relayer 名称、HTTPS 服务地址、手续费率及质押金额，然后提交交易。

### 收益

注册为 relayer 后，你可以获得：

* **Relayer Fee**：你自定义的手续费率（最高 10%），来自你处理的每笔提款
* **Platform Fee（SOL）**：你会预先收到平台手续费中的 SOL 部分
* **Token Deduction**：平台手续费对应的代币价值会从你质押的 ∅ 代币中扣除并发送到 DAO treasury

> **示例**：如果你处理一笔 10 SOL 提款，relayer fee 为 0.1%，DAO fee 为 0.3%：
>
> * 你收到：0.01 SOL（relayer fee）+ 0.03 SOL（DAO fee）= **0.04 SOL**
> * 你的质押减少：价值 0.03 SOL 的 ∅ 代币（基于 oracle 价格）
> * 用户收到：9.96 SOL

### 🎯 Relayer 选择机制

Voidify 使用智能的加权随机选择算法，为每笔提款交易自动选择最合适的 relayer。这在成本效率、可靠性和去中心化之间取得平衡。

#### Relayer 如何被选择

当用户发起提款时，系统会：

1. **筛选活跃 Relayer**：只考虑以下 relayer：
   * 已在链上注册且处于活跃状态
   * 通过健康检查（API endpoint 可响应）
   * 高于最低质押阈值
2. **计算选择权重**：每个 relayer 会基于以下公式获得分数：

   ```txt
   Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
   ```

   该公式表示：

   * **质押越高** = 被选中的概率越高（更多 skin in the game）
   * **手续费越低** = 被选中的概率越高（对用户更好）
   * 手续费惩罚是二次方，因此会强烈抑制高费率 relayer
3. **加权随机选择**：Relayer 按分数概率被选中
   * 分数为 2 倍的 relayer，被选中的概率也是 2 倍
   * 这可以防止垄断，同时奖励高质量服务

#### 选择示例

**示例 1：两个 Relayer**

* Relayer A：1000 万 ∅ 质押，100 bps（1%）手续费 → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B：500 万 ∅ 质押，50 bps（0.5%）手续费 → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

选择概率：

* Relayer A：61.5%
* Relayer B：38.5%

**示例 2：低手续费优势**

* Relayer A：1000 万 ∅ 质押，10 bps（0.1%）手续费 → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C：1000 万 ∅ 质押，100 bps（1%）手续费 → Score = 10,000,000 × 0.75 = 7,500,000

选择概率：

* Relayer A：57%（低手续费获得明显奖励）
* Relayer C：43%

#### 这种方式的优势

✅ **公平竞争**：具有竞争力费率的新 relayer 可以获得市场份额&#x20;

✅ **质量激励**：更高质押和更低手续费会获得更多业务&#x20;

✅ **去中心化**：防止任何单个 relayer 垄断网络&#x20;

✅ **用户保护**：自动偏向成本更低、资本更充足的 relayer

✅ **透明性**：选择算法开源且可验证

#### 手动选择

如果用户愿意，也可以在界面中手动选择特定 relayer：

* 查看所有活跃 relayer 及其手续费
* 按手续费（从低到高）或质押（从高到低）排序
* 为自己的提款选择任意 relayer

这让用户拥有完全控制权，同时也提供智能默认选项以提高便利性。

### Relayer 管理

注册后，你可以：

* **增加质押**：随时增加质押的 ∅ 代币
* **更新手续费**：修改 relayer 手续费率（最高 10%）
* **更新 URL**：修改服务 endpoint
* **监控统计**：跟踪总处理提款数量、赚取的 SOL 和扣除的代币

### 停用与重新激活

* 如果你的质押低于最低阈值（默认 100 万）（由于 DAO fee 扣除），你会被**自动停用**
* 你可以增加 ∅ 代币，使质押回到最低阈值以上并重新激活
* 被停用的 relayer 在重新激活前不能处理新的提款

### 注销

DAO authority 可以：

* **注销** relayer：返还所有质押代币，并将该 relayer 从网络中移除

***

## Русский

Relayer — это независимые участники протокола Voidify, которые помогают выполнять выводы с сохранением приватности. Отправляя транзакции в блокчейн от имени пользователей, relayer предотвращают связь кошельков вывода с адресами депозитов — не получая доступа к средствам или личности пользователя.

**Ключевые функции и гарантии**

* **Сохранение приватности**: позволяет пользователям выводить средства, не раскрывая собственный адрес кошелька в блокчейне
* **Trustless-работа**: relayer не может изменить, перенаправить или получить доступ к внесенным средствам — все данные транзакции проверяются zero-knowledge proof
* **Поддержка gas**: полезно, когда у кошелька получателя нет SOL для оплаты комиссии транзакции
* **Децентрализованная сеть**: система relayer открыта и управляется сообществом; разработчики протокола не имеют централизованного контроля

{% hint style="info" %}
Relayer являются важной частью модели приватности Voidify — они выступают анонимными трансляторами и сохраняют несвязанность событий депозита и вывода.
{% endhint %}

**Почему relayer важны**

Даже при использовании zero-knowledge proof прямой вывод из собственного кошелька раскрывает ваш публичный ключ в блокчейне. Это возвращает трассируемость и ослабляет приватность.

Relayer решают эту проблему, отправляя вашу транзакцию вывода через собственный адрес — отвязывая вас и от proof, и от трансляции транзакции.

### ⚙️ Как это работает

1. Пользователь создает zero-knowledge proof вывода вне сети
2. Пользователь передает proof и запрос relayer через приватный канал
3. Relayer транслирует транзакцию со своего адреса
4. Средства переводятся на адрес получателя
5. Relayer получает определенную протоколом комиссию, включенную в транзакцию

На протяжении всего процесса relayer не знает источник, личность или намерение пользователя, сохраняя полную операционную приватность.

### 🚀 Как стать Relayer

#### Требования

Чтобы зарегистрироваться как relayer, необходимо:

* **Застейкать ∅ токены**: при первой регистрации требуется минимальная сумма стейка (настраивается DAO, обычно 10M ∅)
* **Указать уникальное имя**: 3–32 символа, строчные буквы/цифры + дефис/подчеркивание
* **Указать service URL**: endpoint relayer, куда пользователи отправляют запросы на вывод
* **Установить комиссию**: выбрать relayer fee (максимум 10%)
* **Сервер**: достаточно 2 GB памяти
* **Оставаться активным**: минимальный порог активности (настраивается DAO, обычно 1M ∅)

#### Процесс регистрации

##### **1. Подготовьте сервер**

Получите VPS или выделенный сервер с минимум 2 GB RAM. Подойдет любой Linux-дистрибутив, рекомендуется Ubuntu.

##### **2. Направьте домен на сервер**

Добавьте DNS **A record**, указывающий ваш домен (например, `relayer.example.com`) на публичный IP сервера:

| Type | Name | Value |
| --- | --- | --- |
| A | relayer | `YOUR_SERVER_IP` |

Дождитесь распространения DNS, обычно несколько минут, иногда до 24 часов.

##### **3. Установите Docker на Ubuntu**

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

##### **4. Загрузите и настройте Relayer**

Клонируйте репозиторий Docker-развертывания:

```bash
git clone https://github.com/VoidifyCommunity/voidify-relayer.git voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Репозиторий Docker-развертывания: [https://github.com/VoidifyCommunity/voidify-relayer](https://github.com/VoidifyCommunity/voidify-relayer)
{% endhint %}

Измените `.env`, указав домен и один из вариантов ключа relayer:

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

Или используйте JSON-файл keypair:

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

##### **5. Запустите Relayer**

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy автоматически включает HTTPS для домена, указанного в `.env`.

##### **6. Зарегистрируйтесь on-chain**

После запуска relayer и доступности сервиса через HTTPS зарегистрируйтесь on-chain во frontend(voidify.4sol.xyz)\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

Регистрация relayer уже доступна на [https://voidify.4sol.xyz](https://voidify.4sol.xyz).

Укажите имя relayer, HTTPS-адрес сервиса, ставку комиссии и сумму стейка, затем отправьте транзакцию.

### Что вы зарабатываете

Как зарегистрированный relayer, вы получаете:

* **Relayer Fee**: ваша индивидуальная ставка комиссии (до 10%) за каждый обработанный вывод
* **Platform Fee (в SOL)**: вы заранее получаете часть комиссии платформы в SOL
* **Token Deduction**: токеновый эквивалент platform fee списывается из ваших застейканных ∅ токенов и отправляется в DAO treasury

> **Пример**: если вы обрабатываете вывод 10 SOL с relayer fee 0.1% и DAO fee 0.3%:
>
> * Вы получаете: 0.01 SOL (relayer fee) + 0.03 SOL (DAO fee) = **0.04 SOL**
> * Ваш стейк уменьшается на: ∅ токены стоимостью 0.03 SOL (по oracle price)
> * Пользователь получает: 9.96 SOL

### 🎯 Механизм выбора Relayer

Voidify использует интеллектуальный weighted random selection algorithm для автоматического выбора оптимального relayer для каждой транзакции вывода. Это обеспечивает баланс между стоимостью, надежностью и децентрализацией.

#### Как выбираются Relayer

Когда пользователь инициирует вывод, система:

1. **Фильтрует активных Relayer**: учитываются только relayer, которые:
   * зарегистрированы и активны on-chain
   * проходят health checks (отзывчивые API endpoints)
   * выше минимального порога стейка
2. **Рассчитывает вес выбора**: каждый relayer получает score:

   ```txt
   Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
   ```

   Формула означает:

   * **Больше стейк** = выше вероятность выбора
   * **Ниже комиссия** = выше вероятность выбора
   * Штраф за комиссию квадратичный, поэтому relayer с высокой комиссией сильно невыгодны
3. **Weighted Random Selection**: relayer выбираются вероятностно на основе score
   * Relayer со score в 2 раза выше имеет в 2 раза больше шанс выбора
   * Это предотвращает монополизацию и вознаграждает качественный сервис

#### Примеры выбора

**Пример 1: два Relayer**

* Relayer A: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B: 5M ∅ stake, 50 bps (0.5%) fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

Вероятность выбора:

* Relayer A: 61.5%
* Relayer B: 38.5%

**Пример 2: преимущество низкой комиссии**

* Relayer A: 10M ∅ stake, 10 bps (0.1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × 0.75 = 7,500,000

Вероятность выбора:

* Relayer A: 57% (значительно вознаграждается за низкую комиссию)
* Relayer C: 43%

#### Преимущества подхода

✅ **Честная конкуренция**: новые relayer с конкурентными комиссиями могут получить долю рынка&#x20;

✅ **Стимул качества**: больший стейк и более низкие комиссии получают больше работы&#x20;

✅ **Децентрализация**: предотвращает доминирование одного relayer в сети&#x20;

✅ **Защита пользователей**: автоматически предпочитает экономичных и хорошо капитализированных relayer

✅ **Прозрачность**: алгоритм выбора open-source и проверяемый

#### Ручной выбор

Пользователи также могут вручную выбрать конкретного relayer в интерфейсе:

* Просматривать всех активных relayer и их комиссии
* Сортировать по комиссии (сначала низкая) или стейку (сначала высокий)
* Выбрать любого relayer для своего вывода

Это дает пользователям полный контроль и одновременно предоставляет удобные интеллектуальные defaults.

### Управление Relayer

После регистрации вы можете:

* **Добавить Stake**: увеличить застейканные ∅ токены в любое время
* **Обновить Fee**: изменить ставку relayer fee (максимум 10%)
* **Обновить URL**: изменить service endpoint
* **Мониторить Stats**: отслеживать обработанные выводы, заработанные SOL и списанные токены

### Деактивация и реактивация

* Если ваш стейк падает ниже минимального порога (по умолчанию 1M) из-за DAO fee deductions, вы **автоматически деактивируетесь**
* Вы можете реактивироваться, добавив больше ∅ токенов выше минимального порога
* Деактивированные relayer не могут обрабатывать новые выводы до реактивации

### Unregistration

DAO authority может:

* **Unregister** relayer: возвращает все застейканные токены и удаляет relayer из сети

***

## 日本語

Relayer は Voidify プロトコル内の独立した参加者であり、プライバシーを保護した出金を支援します。ユーザーに代わってブロックチェーンへトランザクションを送信することで、出金ウォレットと入金アドレスの関連付けを防ぎます。ユーザーの資金や身元にアクセスすることはありません。

**主な機能と保証**

* **プライバシー保護**：ユーザーが自分のウォレットアドレスをオンチェーンで公開せずに出金できます
* **Trustless Operation**：Relayer は資金を変更、転送先変更、アクセスできません。すべてのトランザクションデータは zero-knowledge proof によって検証されます
* **Gas サポート**：受取ウォレットにトランザクション手数料用 SOL がない場合に有用です
* **分散型ネットワーク**：relayer システムはオープンでコミュニティ運営です。プロトコル開発者による中央集権的な制御はありません

{% hint style="info" %}
Relayer は Voidify のプライバシーモデルに不可欠です。匿名のブロードキャスターとして、入金イベントと出金イベントの unlinkability を維持します。
{% endhint %}

**Relayer が重要な理由**

Zero-knowledge proof を使用していても、自分のウォレットから直接出金すると、公開鍵がオンチェーンで露出します。これにより追跡可能性が再び生まれ、プライバシーが損なわれます。

Relayer は自身のアドレスから出金トランザクションを送信することで、ユーザーを proof とトランザクションブロードキャストの両方から切り離します。

### ⚙️ 動作の流れ

1. ユーザーがオフチェーンで zero-knowledge withdrawal proof を生成します
2. ユーザーが proof とリクエストを private channel 経由で relayer に送信します
3. Relayer が自身のアドレスからトランザクションをブロードキャストします
4. 資金が受取アドレスへ転送されます
5. Relayer がトランザクションに含まれるプロトコル定義の手数料を受け取ります

このプロセス全体で、relayer はユーザーの出所、身元、意図を知ることがなく、完全な運用上のプライバシーが維持されます。

### 🚀 Relayer になる

#### 要件

Relayer として登録するには、以下が必要です。

* **∅ トークンをステーク**：初回登録には最低ステーク量が必要です（DAO が設定、通常 10M ∅）
* **一意の名前を提供**：3–32 文字、小文字英数字 + ハイフン/アンダースコア
* **サービス URL を提供**：ユーザーが出金リクエストを送信する relayer endpoint
* **手数料率を設定**：relayer fee を選択（最大 10%）
* **サーバー**：2 GB メモリで十分です
* **アクティブ状態を維持**：最小しきい値（DAO が設定、通常 1M ∅）

#### 登録プロセス

##### **1. サーバーを準備**

少なくとも 2 GB RAM の VPS または専用サーバーを用意します。任意の Linux ディストリビューションで動作しますが、Ubuntu を推奨します。

##### **2. ドメインをサーバーに向ける**

DNS **A record** を追加し、ドメイン（例：`relayer.example.com`）をサーバーの public IP address に向けます。

| Type | Name | Value |
| --- | --- | --- |
| A | relayer | `YOUR_SERVER_IP` |

DNS の反映を待ちます。通常は数分、最大 24 時間かかる場合があります。

##### **3. Ubuntu に Docker をインストール**

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

##### **4. Relayer をダウンロードして設定**

Docker デプロイ用リポジトリを clone します。

```bash
git clone https://github.com/VoidifyCommunity/voidify-relayer.git voidify-relayer
cd voidify-relayer
cp .env.example .env
```

{% hint style="info" %}
Docker デプロイ用リポジトリ：[https://github.com/VoidifyCommunity/voidify-relayer](https://github.com/VoidifyCommunity/voidify-relayer)
{% endhint %}

`.env` を編集し、ドメインといずれかの relayer キー設定を入力します。

```dotenv
DOMAIN=relayer.example.com
VOIDIFY_KEYPAIR_BASE58=your_base58_private_key
```

または、keypair JSON ファイルを使用します。

```dotenv
DOMAIN=relayer.example.com
RELAYER_KEYPAIR_FILE=/absolute/path/to/relayer-keypair.json
```

##### **5. Relayer を実行**

```bash
docker compose build
docker compose up -d
docker compose logs -f
```

Caddy は `.env` で指定されたドメインに対して HTTPS を自動的に提供します。

##### **6. オンチェーン登録**

Relayer サービスが起動し HTTPS でアクセスできる状態になったら、frontend(voidify.4sol.xyz) でオンチェーン登録します。\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

Relayer の登録は [https://voidify.4sol.xyz](https://voidify.4sol.xyz) で利用できます。

Relayer 名、HTTPS endpoint、手数料率、ステーク量を入力し、トランザクションを送信します。

### 得られる報酬

登録済み relayer として、以下を得られます。

* **Relayer Fee**：処理する各出金に対するカスタム手数料率（最大 10%）
* **Platform Fee（SOL）**：プラットフォーム手数料部分を SOL で前払い受取
* **Token Deduction**：platform fee に相当するトークン価値がステーク済み ∅ トークンから差し引かれ、DAO treasury に送られます

> **例**：10 SOL の出金を relayer fee 0.1%、DAO fee 0.3% で処理する場合：
>
> * 受取額：0.01 SOL（relayer fee）+ 0.03 SOL（DAO fee）= **0.04 SOL**
> * ステーク減少：0.03 SOL 相当の ∅ トークン（oracle price に基づく）
> * ユーザー受取額：9.96 SOL

### 🎯 Relayer 選択メカニズム

Voidify は、各出金トランザクションに最適な relayer を自動選択するため、intelligent weighted random selection algorithm を実装しています。これにより、コスト効率、信頼性、分散性のバランスを取ります。

#### Relayer の選択方法

ユーザーが出金を開始すると、システムは：

1. **アクティブな Relayer をフィルタ**：以下の relayer のみを対象にします。
   * オンチェーンで登録済みかつアクティブ
   * health checks に合格（API endpoint が応答）
   * 最小ステークしきい値を上回る
2. **選択重みを計算**：各 relayer は以下に基づいて score を受け取ります。

   ```txt
   Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
   ```

   この式の意味：

   * **ステークが高い** = 選択確率が高い
   * **手数料が低い** = 選択確率が高い
   * 手数料ペナルティは二次関数なので、高手数料 relayer は強く抑制されます
3. **Weighted Random Selection**：Relayer は score に基づく確率で選ばれます
   * score が 2 倍の relayer は、選ばれる確率も 2 倍です
   * 独占を防ぎつつ、質の高いサービスを報酬します

#### 選択例

**例 1：2 つの Relayer**

* Relayer A：10M ∅ stake、100 bps（1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B：5M ∅ stake、50 bps（0.5%）fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

選択確率：

* Relayer A：61.5%
* Relayer B：38.5%

**例 2：低手数料の優位性**

* Relayer A：10M ∅ stake、10 bps（0.1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C：10M ∅ stake、100 bps（1%）fee → Score = 10,000,000 × 0.75 = 7,500,000

選択確率：

* Relayer A：57%（低手数料が大きく評価されます）
* Relayer C：43%

#### この方式の利点

✅ **公平な競争**：競争力のある手数料の新しい relayer が市場シェアを得られます&#x20;

✅ **品質インセンティブ**：高いステークと低い手数料はより多くの仕事で報酬されます&#x20;

✅ **分散性**：単一 relayer がネットワークを支配することを防ぎます&#x20;

✅ **ユーザー保護**：コスト効率が高く、十分な資本を持つ relayer を自動的に優先します

✅ **透明性**：選択アルゴリズムは open-source で検証可能です

#### 手動選択

ユーザーは希望すれば、インターフェースから特定の relayer を手動で選択できます。

* すべてのアクティブ relayer とその手数料を表示
* 手数料（低い順）またはステーク（高い順）で並べ替え
* 出金に任意の relayer を選択

これにより、ユーザーは完全な制御を持ちつつ、便利な intelligent defaults も利用できます。

### Relayer 管理

登録後、以下ができます。

* **Stake 追加**：ステーク済み ∅ トークンをいつでも増やす
* **Fee 更新**：relayer fee rate を変更（最大 10%）
* **URL 更新**：service endpoint を変更
* **Stats 監視**：処理した出金総数、獲得 SOL、差し引かれたトークンを追跡

### 無効化と再有効化

* DAO fee deductions によりステークが最小しきい値（デフォルト 1M）を下回ると、**自動的に無効化**されます
* ∅ トークンを追加してステークを最小値以上に戻すと再有効化できます
* 無効化された relayer は、再有効化されるまで新しい出金を処理できません

### 登録解除

DAO authority は以下を実行できます。

* **Relayer の登録解除**：すべてのステーク済みトークンを返却し、その relayer をネットワークから削除します
