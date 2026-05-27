---
description: What Is a Relayer?
---

# V. Voidify Relayers

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

***

## English

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

Relayers are independent participants within the Voidify protocol who help facilitate privacy-preserving withdrawals. By submitting transactions to the blockchain on behalf of users, relayers prevent withdrawal wallets from being linked to deposit addresses — all without ever accessing user funds or identities.

***

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

***

## ⚙️ How It Works

1. The user generates a zero-knowledge withdrawal proof off-chain
2. The user transmits the proof and request to a relayer via a private channel
3. The relayer broadcasts the transaction from their own address
4. Funds are transferred to the recipient address
5. The relayer receives a protocol-defined fee included in the transaction

Throughout this process, the relayer never knows the origin, identity, or intent of the user — preserving full operational privacy.

***

## 🚀 Becoming a Relayer

### Requirements

To register as a relayer, you must:

* **Stake ∅ tokens**: A minimum stake amount is required for the first time(configurable by DAO, typically 10M ∅ tokens)
* **Provide a unique name**: 3–32 characters, lowercase alphanumeric + hyphen/underscore
* **Provide a service URL**: Your relayer endpoint where users can submit withdrawal requests
* **Set your fee rate**: Choose your relayer fee (max 10%)
* **Server** (2 GB of memory is enough)
* **Stay active**: minimum threshold(configurable by DAO, typically 1M ∅ tokens)

### Registration Process

#### **1. Prepare a Server**

Get a VPS or dedicated server with at least 2 GB RAM. Any Linux distribution works (Ubuntu recommended).

#### **2. Point a Domain to Your Server**

Add a DNS **A record** pointing your domain (e.g. `relayer.example.com`) to your server's public IP address:

| Type | Name    | Value            |
| ---- | ------- | ---------------- |
| A    | relayer | `YOUR_SERVER_IP` |

Wait for DNS propagation (usually a few minutes, up to 24 hours).

#### **3. Install Nginx**

```bash
sudo apt update
sudo apt install -y nginx
```

#### **4. Configure Nginx Reverse Proxy**

Create a config file for your relayer:

```bash
sudo nano /etc/nginx/sites-available/relayer
```

Paste the following (replace `relayer.example.com` with your domain):

```nginx
server {
    listen 80;
    server_name relayer.example.com;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable the site and restart Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/relayer /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### **5. Enable HTTPS with Certbot**

Install Certbot and obtain a free SSL certificate from Let's Encrypt:

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d relayer.example.com
```

Follow the prompts to complete certificate issuance. Certbot will automatically update your Nginx config to serve HTTPS.

Verify auto-renewal is set up:

```bash
sudo certbot renew --dry-run
```

Your relayer endpoint is now accessible at `https://relayer.example.com`.

#### **6. Download and Configure the Relayer**

Download the latest release from [GitHub Releases](https://github.com/VoidifyCommunity/voidify-relayer/releases):

```bash
wget https://github.com/user-attachments/files/26513398/voidify-relayer-release.zip
unzip voidify-relayer-release.zip
cd voidify-relayer-release
```

Set up the environment:

```bash
cp .env.example .env
```

Edit `.env` and fill in `RELAYER_PRIVATE_KEY` with your Base58-encoded Solana private key.

{% hint style="info" %}
Use the private key of a wallet intended for testing. The code will be open-sourced when it goes live on mainnet
{% endhint %}

#### **7. Run the Relayer**

```bash
# Start in a screen session so it keeps running after you disconnect
screen -S relayer
./voidify-relayer

# Detach from screen: press Ctrl+A then D
# Re-attach later:
screen -r relayer
```

#### **8. Register On-Chain**

Once your relayer service is running and accessible via HTTPS, register on-chain on frontend(voidify.4sol.xyz)\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

***

## What You Earn

As a registered relayer, you earn:

* **Relayer Fee**: Your custom fee rate (up to 10%) on every withdrawal you process
* **Platform Fee (in SOL)**: You receive the platform's fee portion in SOL upfront
* **Token Deduction**: The platform fee's token equivalent is deducted from your staked ∅ tokens and sent to the DAO treasury

> **Example**: If you process a 10 SOL withdrawal with a 0.1% relayer fee and 0.3% DAO fee:
>
> * You receive: 0.01 SOL (relayer fee) + 0.03 SOL (DAO fee) = **0.04 SOL**
> * Your stake is reduced by: 0.03 SOL worth of ∅ tokens (based on oracle price)
> * User receives: 9.96 SOL

## 🎯 Relayer Selection Mechanism

Voidify implements an intelligent, weighted random selection algorithm to automatically choose the optimal relayer for each withdrawal transaction. This ensures a balance between cost-efficiency, reliability, and decentralization.

### How Relayers Are Selected

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

### Selection Examples

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

### Benefits of This Approach

✅ **Fair Competition**: New relayers with competitive fees can gain market share&#x20;

✅ **Quality Incentive**: Higher stakes and lower fees are rewarded with more business&#x20;

✅ **Decentralization**: Prevents any single relayer from dominating the network&#x20;

✅ **User Protection**: Automatically favors cost-effective, well-capitalized relayers

✅ **Transparency**: Selection algorithm is open-source and verifiable

### Manual Selection

Users can also manually choose a specific relayer from the interface if they prefer:

* View all active relayers with their fees
* Sort by fee (lowest first) or stake (highest first)
* Select any relayer for their withdrawal

This gives users full control while providing intelligent defaults for convenience.

***

## Relayer Management

Once registered, you can:

* **Add Stake**: Increase your staked ∅ tokens at any time
* **Update Fee**: Change your relayer fee rate (max 10%)
* **Update URL**: Change your service endpoint
* **Monitor Stats**: Track your total withdrawals processed, SOL earned, and tokens deducted

## Deactivation & Reactivation

* If your stake drops below the minimum threshold(default 1M) (due to DAO fee deductions), you are **automatically deactivated**
* You can reactivate by adding more ∅ tokens to bring your stake above the minimum
* Deactivated relayers cannot process new withdrawals until reactivated

## Unregistration

The DAO authority can:

* **Unregister** a relayer: Returns all staked tokens and removes the relayer from the network

<br>

***

## 中文

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

Relayers 是 Voidify 协议中的独立参与者，帮助完成保护隐私的提款。Relayer 代表用户向区块链提交交易，从而防止提款钱包与存款地址被关联，并且在整个过程中不会访问用户资金或身份。

***

**核心功能与保证**

* **保护隐私**：允许用户提款，而不在链上暴露自己的钱包地址
* **无需信任的运行**：Relayers 无法修改、重定向或访问已存入资金；所有交易数据都由零知识证明验证
* **Gas 支持**：当收款钱包没有 SOL 支付交易费时非常有用
* **去中心化网络**：Relayer 系统开放且由社区运行；协议开发者没有中心化控制权

{% hint style="info" %}
Relayers 是 Voidify 隐私模型的关键部分，它们作为匿名广播者，维持存款事件与提款事件之间的不可链接性。
{% endhint %}

**为什么 Relayers 很重要**

即使有零知识证明，如果你直接用自己的钱包提款，你的公钥仍会暴露在链上。这会重新引入可追踪性，并削弱隐私。

Relayers 通过自己的地址提交你的提款交易，解决了这个问题，让你同时与证明和交易广播解除关联。

***

## ⚙️ 工作原理

1. 用户在链下生成零知识提款证明
2. 用户通过私密通道将证明和请求发送给 relayer
3. Relayer 用自己的地址广播交易
4. 资金转移到收款地址
5. Relayer 收取交易中包含的协议定义费用

在整个过程中，relayer 永远不知道用户的来源、身份或意图，从而保持完整的操作隐私。

***

## 🚀 成为 Relayer

### 要求

要注册为 relayer，你必须：

* **质押 ∅ tokens**：首次需要最低质押数量（由 DAO 配置，通常为 10M ∅ tokens）
* **提供唯一名称**：3–32 个字符，小写字母数字 + 连字符/下划线
* **提供服务 URL**：你的 relayer endpoint，用户可向其提交提款请求
* **设置费率**：选择你的 relayer fee（最高 10%）
* **服务器**（2 GB 内存足够）
* **保持活跃**：最低阈值（由 DAO 配置，通常为 1M ∅ tokens）

### 注册流程

#### **1. 准备服务器**

准备一台至少 2 GB RAM 的 VPS 或专用服务器。任何 Linux 发行版都可以（推荐 Ubuntu）。

#### **2. 将域名指向服务器**

添加 DNS **A record**，将你的域名（例如 `relayer.example.com`）指向服务器公网 IP：

| Type | Name    | Value            |
| ---- | ------- | ---------------- |
| A    | relayer | `YOUR_SERVER_IP` |

等待 DNS 传播（通常几分钟，最长可达 24 小时）。

#### **3. 安装 Nginx**

```bash
sudo apt update
sudo apt install -y nginx
```

#### **4. 配置 Nginx 反向代理**

为你的 relayer 创建配置文件：

```bash
sudo nano /etc/nginx/sites-available/relayer
```

粘贴以下内容（将 `relayer.example.com` 替换为你的域名）：

```nginx
server {
    listen 80;
    server_name relayer.example.com;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

启用站点并重启 Nginx：

```bash
sudo ln -s /etc/nginx/sites-available/relayer /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### **5. 使用 Certbot 启用 HTTPS**

安装 Certbot，并从 Let's Encrypt 获取免费 SSL 证书：

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d relayer.example.com
```

按提示完成证书签发。Certbot 会自动更新你的 Nginx 配置以提供 HTTPS。

验证自动续期已设置：

```bash
sudo certbot renew --dry-run
```

你的 relayer endpoint 现在可通过 `https://relayer.example.com` 访问。

#### **6. 下载并配置 Relayer**

从 [GitHub Releases](https://github.com/VoidifyCommunity/voidify-relayer/releases) 下载最新 release：

```bash
wget https://github.com/user-attachments/files/26513398/voidify-relayer-release.zip
unzip voidify-relayer-release.zip
cd voidify-relayer-release
```

设置环境：

```bash
cp .env.example .env
```

编辑 `.env`，并用你的 Base58 编码 Solana private key 填写 `RELAYER_PRIVATE_KEY`。

{% hint style="info" %}
使用专门用于测试的钱包私钥。代码在 mainnet 上线时会开源
{% endhint %}

#### **7. 运行 Relayer**

```bash
# 在 screen session 中启动，这样断开连接后仍会继续运行
screen -S relayer
./voidify-relayer

# 从 screen 分离：按 Ctrl+A 然后按 D
# 之后重新连接：
screen -r relayer
```

#### **8. 链上注册**

当你的 relayer 服务已运行并可通过 HTTPS 访问后，在 frontend(voidify.4sol.xyz) 上进行链上注册\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

***

## 你能获得什么

作为注册 relayer，你可以获得：

* **Relayer Fee**：你自定义的费率（最高 10%），来自你处理的每笔提款
* **Platform Fee（SOL）**：你会预先收到平台费用中以 SOL 计价的部分
* **Token Deduction**：平台费的 token 等价值会从你质押的 ∅ tokens 中扣除，并发送到 DAO treasury

> **示例**：如果你处理一笔 10 SOL 提款，relayer fee 为 0.1%，DAO fee 为 0.3%：
>
> * 你收到：0.01 SOL（relayer fee）+ 0.03 SOL（DAO fee）= **0.04 SOL**
> * 你的 stake 减少：价值 0.03 SOL 的 ∅ tokens（基于 oracle price）
> * 用户收到：9.96 SOL

## 🎯 Relayer 选择机制

Voidify 实现了一种智能的加权随机选择算法，用于为每笔提款交易自动选择最优 relayer。这确保了成本效率、可靠性和去中心化之间的平衡。

### Relayers 如何被选择

当用户发起提款时，系统会：

1. **过滤活跃 Relayers**：只考虑满足以下条件的 relayers：
   * 已在链上注册且处于活跃状态
   * 通过健康检查（API endpoints 可响应）
   * 高于最低质押阈值
2.  **计算选择权重**：每个 relayer 会根据以下公式获得分数：

    ```txt
    Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
    ```

    该公式意味着：

    * **更高 stake** = 更高被选中概率（更多利益绑定）
    * **更低 fees** = 更高被选中概率（对用户更好）
    * 费用惩罚是二次方，因此强烈抑制高费率 relayers
3. **加权随机选择**：Relayers 会根据分数以概率方式被选中
   * 分数为 2 倍的 relayer 被选中概率也是 2 倍
   * 这防止垄断，同时奖励高质量服务

### 选择示例

**示例 1：两个 Relayers**

* Relayer A：10M ∅ stake，100 bps（1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B：5M ∅ stake，50 bps（0.5%）fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

选择概率：

* Relayer A：61.5% chance
* Relayer B：38.5% chance

**示例 2：低费率优势**

* Relayer A：10M ∅ stake，10 bps（0.1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C：10M ∅ stake，100 bps（1%）fee → Score = 10,000,000 × 0.75 = 7,500,000

选择概率：

* Relayer A：57% chance（因更低费率获得显著奖励）
* Relayer C：43% chance

### 这种方式的好处

✅ **公平竞争**：有竞争力费率的新 relayers 可以获得市场份额&#x20;

✅ **质量激励**：更高 stake 和更低 fees 会获得更多业务&#x20;

✅ **去中心化**：防止单个 relayer 主导网络&#x20;

✅ **用户保护**：自动偏向成本更低、资金更充足的 relayers

✅ **透明性**：选择算法开源且可验证

### 手动选择

用户也可以在界面中手动选择特定 relayer：

* 查看所有活跃 relayers 及其 fees
* 按 fee（从低到高）或 stake（从高到低）排序
* 为自己的提款选择任意 relayer

这既让用户拥有完全控制权，也提供了方便的智能默认值。

***

## Relayer 管理

注册后，你可以：

* **Add Stake**：随时增加质押的 ∅ tokens
* **Update Fee**：修改你的 relayer fee rate（最高 10%）
* **Update URL**：修改你的 service endpoint
* **Monitor Stats**：跟踪你处理的总提款数、赚取的 SOL 和扣除的 tokens

## 停用与重新激活

* 如果你的 stake 低于最低阈值（默认 1M）（由于 DAO fee deductions），你会被**自动停用**
* 你可以通过添加更多 ∅ tokens 使 stake 回到最低值以上来重新激活
* 停用的 relayers 在重新激活前无法处理新的提款

## 注销

DAO authority 可以：

* **Unregister** 一个 relayer：返还所有 staked tokens，并将该 relayer 从网络中移除

<br>

***

## Русский

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

Relayers — независимые участники протокола Voidify, которые помогают выполнять выводы с сохранением приватности. Отправляя транзакции в блокчейн от имени пользователей, relayers предотвращают связывание кошельков вывода с адресами депозита — при этом они никогда не получают доступ к средствам или личности пользователя.

***

**Ключевые функции и гарантии**

* **Сохранение приватности**: позволяет пользователям выводить средства, не раскрывая собственный адрес кошелька ончейн
* **Trustless Operation**: Relayers не могут изменять, перенаправлять или получать доступ к внесенным средствам — все данные транзакции проверяются zero-knowledge proofs
* **Gas Support**: полезно, когда у кошелька получателя нет SOL для оплаты transaction fees
* **Децентрализованная сеть**: система relayer открыта и управляется сообществом; разработчики протокола не имеют централизованного контроля

{% hint style="info" %}
Relayers необходимы для модели приватности Voidify: они выступают анонимными broadcasters, поддерживая несвязываемость между событиями депозита и вывода.
{% endhint %}

**Почему Relayers важны**

Даже с zero-knowledge proofs прямой вывод из собственного кошелька раскрывает ваш public key ончейн. Это возвращает трассируемость и ослабляет приватность.

Relayers решают эту проблему, отправляя вашу транзакцию вывода со своего адреса, отсоединяя вас и от proof, и от transaction broadcast.

***

## ⚙️ Как это работает

1. Пользователь создает zero-knowledge withdrawal proof офчейн
2. Пользователь передает proof и request relayer через private channel
3. Relayer транслирует транзакцию со своего адреса
4. Средства переводятся на адрес получателя
5. Relayer получает protocol-defined fee, включенную в транзакцию

На протяжении всего процесса relayer никогда не знает источник, личность или намерение пользователя, сохраняя полную operational privacy.

***

## 🚀 Как стать Relayer

### Требования

Чтобы зарегистрироваться как relayer, вы должны:

* **Застейкать ∅ tokens**: для первого раза требуется минимальный stake amount (настраивается DAO, обычно 10M ∅ tokens)
* **Предоставить уникальное имя**: 3–32 символа, lowercase alphanumeric + hyphen/underscore
* **Предоставить service URL**: ваш relayer endpoint, куда пользователи могут отправлять withdrawal requests
* **Установить fee rate**: выберите relayer fee (максимум 10%)
* **Server** (2 GB памяти достаточно)
* **Оставаться активным**: minimum threshold (настраивается DAO, обычно 1M ∅ tokens)

### Процесс регистрации

#### **1. Подготовьте сервер**

Получите VPS или dedicated server минимум с 2 GB RAM. Подойдет любой Linux distribution (рекомендуется Ubuntu).

#### **2. Направьте домен на сервер**

Добавьте DNS **A record**, указывающий ваш домен (например, `relayer.example.com`) на public IP вашего сервера:

| Type | Name    | Value            |
| ---- | ------- | ---------------- |
| A    | relayer | `YOUR_SERVER_IP` |

Дождитесь распространения DNS (обычно несколько минут, до 24 часов).

#### **3. Установите Nginx**

```bash
sudo apt update
sudo apt install -y nginx
```

#### **4. Настройте Nginx Reverse Proxy**

Создайте config file для вашего relayer:

```bash
sudo nano /etc/nginx/sites-available/relayer
```

Вставьте следующее (замените `relayer.example.com` вашим доменом):

```nginx
server {
    listen 80;
    server_name relayer.example.com;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Включите site и перезапустите Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/relayer /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### **5. Включите HTTPS через Certbot**

Установите Certbot и получите бесплатный SSL certificate от Let's Encrypt:

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d relayer.example.com
```

Следуйте подсказкам, чтобы завершить issuance certificate. Certbot автоматически обновит вашу Nginx config для обслуживания HTTPS.

Проверьте, что auto-renewal настроен:

```bash
sudo certbot renew --dry-run
```

Ваш relayer endpoint теперь доступен по `https://relayer.example.com`.

#### **6. Скачайте и настройте Relayer**

Скачайте последний release из [GitHub Releases](https://github.com/VoidifyCommunity/voidify-relayer/releases):

```bash
wget https://github.com/user-attachments/files/26513398/voidify-relayer-release.zip
unzip voidify-relayer-release.zip
cd voidify-relayer-release
```

Настройте environment:

```bash
cp .env.example .env
```

Отредактируйте `.env` и заполните `RELAYER_PRIVATE_KEY` вашим Base58-encoded Solana private key.

{% hint style="info" %}
Используйте private key кошелька, предназначенного для тестирования. Код будет open-sourced, когда он выйдет в mainnet
{% endhint %}

#### **7. Запустите Relayer**

```bash
# Запустите в screen session, чтобы процесс продолжал работать после отключения
screen -S relayer
./voidify-relayer

# Отсоединиться от screen: нажмите Ctrl+A, затем D
# Подключиться позже:
screen -r relayer
```

#### **8. Зарегистрируйтесь ончейн**

Когда ваш relayer service запущен и доступен через HTTPS, зарегистрируйтесь ончейн на frontend(voidify.4sol.xyz)\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

***

## Что вы зарабатываете

Как зарегистрированный relayer, вы зарабатываете:

* **Relayer Fee**: ваш custom fee rate (до 10%) на каждом выводе, который вы обрабатываете
* **Platform Fee (in SOL)**: вы получаете portion of platform fee в SOL заранее
* **Token Deduction**: token equivalent platform fee списывается из ваших staked ∅ tokens и отправляется в DAO treasury

> **Пример**: если вы обрабатываете вывод 10 SOL с relayer fee 0.1% и DAO fee 0.3%:
>
> * Вы получаете: 0.01 SOL (relayer fee) + 0.03 SOL (DAO fee) = **0.04 SOL**
> * Ваш stake уменьшается на: ∅ tokens стоимостью 0.03 SOL (based on oracle price)
> * Пользователь получает: 9.96 SOL

## 🎯 Механизм выбора Relayer

Voidify реализует интеллектуальный weighted random selection algorithm, который автоматически выбирает оптимального relayer для каждой withdrawal transaction. Это обеспечивает баланс между cost-efficiency, reliability и decentralization.

### Как выбираются Relayers

Когда пользователь инициирует вывод, система:

1. **Фильтрует активных Relayers**: учитываются только relayers, которые:
   * зарегистрированы и активны ончейн
   * проходят health checks (responsive API endpoints)
   * выше minimum stake threshold
2.  **Рассчитывает Selection Weight**: каждый relayer получает score на основе:

    ```txt
    Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
    ```

    Эта формула означает:

    * **Higher stake** = Higher selection probability (больше skin in the game)
    * **Lower fees** = Higher selection probability (лучше для пользователей)
    * Штраф за fee квадратичный, поэтому high-fee relayers сильно discouraged
3. **Weighted Random Selection**: Relayers выбираются вероятностно на основе их scores
   * Relayer с score в 2 раза выше имеет в 2 раза больше шансов быть выбранным
   * Это предотвращает monopolization и вознаграждает quality service

### Примеры выбора

**Пример 1: два Relayers**

* Relayer A: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B: 5M ∅ stake, 50 bps (0.5%) fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

Вероятность выбора:

* Relayer A: 61.5% chance
* Relayer B: 38.5% chance

**Пример 2: преимущество низкой fee**

* Relayer A: 10M ∅ stake, 10 bps (0.1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × 0.75 = 7,500,000

Вероятность выбора:

* Relayer A: 57% chance (significantly rewarded for lower fee)
* Relayer C: 43% chance

### Преимущества такого подхода

✅ **Fair Competition**: новые relayers с competitive fees могут получить market share&#x20;

✅ **Quality Incentive**: higher stakes и lower fees вознаграждаются большим business&#x20;

✅ **Decentralization**: предотвращает доминирование одного relayer в сети&#x20;

✅ **User Protection**: автоматически предпочитает cost-effective, well-capitalized relayers

✅ **Transparency**: selection algorithm open-source и verifiable

### Ручной выбор

Пользователи также могут вручную выбрать конкретного relayer в интерфейсе:

* просмотреть всех active relayers и их fees
* сортировать по fee (lowest first) или stake (highest first)
* выбрать любого relayer для своего вывода

Это дает пользователям полный контроль, одновременно предоставляя удобные intelligent defaults.

***

## Управление Relayer

После регистрации вы можете:

* **Add Stake**: увеличить свои staked ∅ tokens в любое время
* **Update Fee**: изменить relayer fee rate (максимум 10%)
* **Update URL**: изменить service endpoint
* **Monitor Stats**: отслеживать общее число обработанных withdrawals, заработанные SOL и списанные tokens

## Деактивация и реактивация

* Если ваш stake падает ниже minimum threshold (default 1M) из-за DAO fee deductions, вы **автоматически деактивируетесь**
* Вы можете реактивироваться, добавив больше ∅ tokens, чтобы вернуть stake выше минимума
* Деактивированные relayers не могут обрабатывать новые withdrawals до реактивации

## Unregistration

DAO authority может:

* **Unregister** relayer: возвращает все staked tokens и удаляет relayer из сети

<br>

***

## 日本語

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

Relayers は Voidify プロトコル内の独立参加者であり、プライバシーを保護した出金を支援します。ユーザーの代わりにブロックチェーンへトランザクションを送信することで、relayers は出金ウォレットが預入アドレスと結び付けられることを防ぎます。その間、ユーザーの資金や身元へアクセスすることはありません。

***

**主な機能と保証**

* **Privacy-Preserving**：ユーザーが自分のウォレットアドレスをオンチェーンで公開せずに出金できるようにします
* **Trustless Operation**：Relayers は預け入れられた資金を変更、転送先変更、またはアクセスできません。すべての transaction data は zero-knowledge proofs によって検証されます
* **Gas Support**：受取ウォレットに transaction fees を支払う SOL がない場合に役立ちます
* **Decentralized Network**：Relayer system はオープンでコミュニティ運営です。Protocol developers は中央集権的な制御を持ちません

{% hint style="info" %}
Relayers は Voidify の privacy model に不可欠です。匿名 broadcasters として機能し、deposit events と withdrawal events の不可リンク性を維持します。
{% endhint %}

**なぜ Relayers が重要か**

Zero-knowledge proofs があっても、自分の wallet から直接出金すると public key がオンチェーンで公開されます。これにより traceability が再導入され、privacy が損なわれます。

Relayers は自分の address からあなたの withdrawal transaction を送信することで、この問題を解決します。これにより、あなたは proof と transaction broadcast の両方から切り離されます。

***

## ⚙️ 仕組み

1. ユーザーがオフチェーンで zero-knowledge withdrawal proof を生成します
2. ユーザーが private channel 経由で proof と request を relayer に送信します
3. Relayer が自分の address から transaction を broadcast します
4. Funds が recipient address に転送されます
5. Relayer は transaction に含まれる protocol-defined fee を受け取ります

この過程で、relayer はユーザーの origin、identity、intent を一切知りません。これにより完全な operational privacy が保たれます。

***

## 🚀 Relayer になる

### 要件

Relayer として登録するには、次が必要です。

* **∅ tokens を stake**：初回には minimum stake amount が必要です（DAO により設定可能、通常 10M ∅ tokens）
* **一意の name を提供**：3–32 文字、小文字英数字 + hyphen/underscore
* **service URL を提供**：ユーザーが withdrawal requests を送信できる relayer endpoint
* **fee rate を設定**：relayer fee を選択（最大 10%）
* **Server**（2 GB memory で十分）
* **active を維持**：minimum threshold（DAO により設定可能、通常 1M ∅ tokens）

### 登録プロセス

#### **1. サーバーを準備する**

少なくとも 2 GB RAM の VPS または dedicated server を用意します。任意の Linux distribution が使えます（Ubuntu 推奨）。

#### **2. ドメインをサーバーへ向ける**

DNS **A record** を追加し、あなたの domain（例：`relayer.example.com`）を server の public IP address へ向けます。

| Type | Name    | Value            |
| ---- | ------- | ---------------- |
| A    | relayer | `YOUR_SERVER_IP` |

DNS propagation を待ちます（通常数分、最大 24 時間）。

#### **3. Nginx をインストールする**

```bash
sudo apt update
sudo apt install -y nginx
```

#### **4. Nginx Reverse Proxy を設定する**

Relayer 用の config file を作成します。

```bash
sudo nano /etc/nginx/sites-available/relayer
```

以下を貼り付けます（`relayer.example.com` をあなたの domain に置き換えてください）。

```nginx
server {
    listen 80;
    server_name relayer.example.com;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Site を有効化し、Nginx を再起動します。

```bash
sudo ln -s /etc/nginx/sites-available/relayer /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### **5. Certbot で HTTPS を有効化する**

Certbot をインストールし、Let's Encrypt から無料 SSL certificate を取得します。

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d relayer.example.com
```

Prompt に従って certificate issuance を完了します。Certbot は HTTPS を提供するように Nginx config を自動更新します。

Auto-renewal が設定されていることを確認します。

```bash
sudo certbot renew --dry-run
```

Relayer endpoint は `https://relayer.example.com` でアクセス可能になります。

#### **6. Relayer をダウンロードして設定する**

[GitHub Releases](https://github.com/VoidifyCommunity/voidify-relayer/releases) から最新 release をダウンロードします。

```bash
wget https://github.com/user-attachments/files/26513398/voidify-relayer-release.zip
unzip voidify-relayer-release.zip
cd voidify-relayer-release
```

Environment を設定します。

```bash
cp .env.example .env
```

`.env` を編集し、Base58-encoded Solana private key を `RELAYER_PRIVATE_KEY` に入力します。

{% hint style="info" %}
Testing 用の wallet の private key を使用してください。Code は mainnet で稼働するときに open-sourced されます
{% endhint %}

#### **7. Relayer を実行する**

```bash
# 切断後も実行を続けるため screen session で開始します
screen -S relayer
./voidify-relayer

# screen から detach：Ctrl+A を押してから D
# 後で re-attach：
screen -r relayer
```

#### **8. オンチェーン登録**

Relayer service が実行され、HTTPS でアクセス可能になったら、frontend(voidify.4sol.xyz) でオンチェーン登録します\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

***

## 得られる報酬

登録済み relayer として、次を得ます。

* **Relayer Fee**：処理する各 withdrawal で、あなたの custom fee rate（最大 10%）
* **Platform Fee (in SOL)**：platform fee の一部を SOL で upfront に受け取ります
* **Token Deduction**：platform fee の token equivalent が staked ∅ tokens から差し引かれ、DAO treasury に送られます

> **例**：0.1% relayer fee と 0.3% DAO fee で 10 SOL withdrawal を処理する場合：
>
> * 受け取る額：0.01 SOL（relayer fee）+ 0.03 SOL（DAO fee）= **0.04 SOL**
> * Stake は次の分だけ減少：0.03 SOL 相当の ∅ tokens（oracle price に基づく）
> * User receives：9.96 SOL

## 🎯 Relayer Selection Mechanism

Voidify は、各 withdrawal transaction に最適な relayer を自動選択するため、intelligent weighted random selection algorithm を実装しています。これにより cost-efficiency、reliability、decentralization のバランスが保たれます。

### Relayers の選択方法

ユーザーが withdrawal を開始すると、system は次を行います。

1. **Active Relayers をフィルタ**：次の条件を満たす relayers のみを考慮します。
   * On-chain で registered and active
   * Health checks に合格（responsive API endpoints）
   * Minimum stake threshold を上回る
2.  **Selection Weight を計算**：各 relayer は次に基づいて score を受け取ります。

    ```txt
    Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
    ```

    この式の意味：

    * **Higher stake** = Higher selection probability（より多くの skin in the game）
    * **Lower fees** = Higher selection probability（ユーザーに有利）
    * Fee penalty は quadratic なので、high-fee relayers は強く抑制されます
3. **Weighted Random Selection**：Relayers は scores に基づいて確率的に選ばれます
   * Score が 2 倍の relayer は、選ばれる chance も 2 倍です
   * これにより monopolization を防ぎ、quality service を報酬化します

### 選択例

**例 1：2 つの Relayers**

* Relayer A：10M ∅ stake、100 bps（1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B：5M ∅ stake、50 bps（0.5%）fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

Selection probability：

* Relayer A：61.5% chance
* Relayer B：38.5% chance

**例 2：低 Fee の優位性**

* Relayer A：10M ∅ stake、10 bps（0.1%）fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C：10M ∅ stake、100 bps（1%）fee → Score = 10,000,000 × 0.75 = 7,500,000

Selection probability：

* Relayer A：57% chance（lower fee により大きく reward される）
* Relayer C：43% chance

### この方式の利点

✅ **Fair Competition**：Competitive fees を持つ新しい relayers が market share を得られます&#x20;

✅ **Quality Incentive**：Higher stakes と lower fees はより多くの business で報酬を受けます&#x20;

✅ **Decentralization**：単一 relayer が network を支配することを防ぎます&#x20;

✅ **User Protection**：Cost-effective で well-capitalized な relayers を自動的に優先します

✅ **Transparency**：Selection algorithm は open-source で verifiable です

### Manual Selection

ユーザーは希望すれば interface から特定の relayer を手動選択することもできます。

* すべての active relayers と fees を表示
* Fee（lowest first）または stake（highest first）で sort
* 自分の withdrawal に任意の relayer を選択

これにより、便利な intelligent defaults を提供しながら、ユーザーは完全な control を持てます。

***

## Relayer Management

登録後、次が可能です。

* **Add Stake**：いつでも staked ∅ tokens を増やす
* **Update Fee**：relayer fee rate を変更（最大 10%）
* **Update URL**：service endpoint を変更
* **Monitor Stats**：処理した total withdrawals、earned SOL、deducted tokens を追跡

## Deactivation & Reactivation

* DAO fee deductions により stake が minimum threshold（default 1M）を下回ると、**automatically deactivated** されます
* Stake が minimum を上回るように ∅ tokens を追加すれば reactivate できます
* Deactivated relayers は reactivated されるまで新しい withdrawals を処理できません

## Unregistration

DAO authority は次を行えます。

* **Unregister** a relayer：すべての staked tokens を返却し、その relayer を network から削除します

<br>
