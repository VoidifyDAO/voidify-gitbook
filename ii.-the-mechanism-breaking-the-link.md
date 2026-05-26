---
description: How Voidify Works
---

# II. The Mechanism: Breaking the Link

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2FMDD8YhvhqGpVn2jmw9pd%2Fvoidify%20astronaut.png?alt=media&#x26;token=f48c2cea-4c25-4fed-98af-29b956398485" alt="" width="275"><figcaption></figcaption></figure>

***

## English

At the core of Voidify’s design are zero-knowledge proofs (zk-SNARKs) and zk-optimized hash functions built to suit Solana’s high-throughput architecture.

***

### Anonymity Pools

Voidify pools are fixed-denomination privacy pools. Each pool accepts one standard deposit amount, such as 0.1 SOL, 1 SOL, or 10 SOL.

A user first deposits into a pool and receives a private note. Later, the user can withdraw the same denomination to a different wallet by generating a zero-knowledge proof. The proof shows that the user owns one valid, unused deposit in the pool, without revealing which deposit it was.

#### Why deposit count matters

More deposits in the same pool create more possible sources for each withdrawal. If a pool has only a few deposits, an observer has fewer candidates to analyze. If a pool has many independent deposits, each withdrawal becomes harder to link to a specific deposit.

For this reason, popular denominations usually provide stronger practical privacy than rarely used denominations.

#### Why timing matters

The time between deposit and withdrawal also affects privacy.

If a user deposits and withdraws shortly afterward, especially when few other deposits happen in between, the withdrawal may be easier to correlate with the recent deposit. Waiting longer allows more deposits to enter the same pool, increasing the number of plausible sources.

A longer delay does not guarantee perfect privacy, but immediate withdrawals usually provide weaker privacy because they create a clearer timing pattern.

***

#### **How Deposits Work**

When a user deposits tokens into Voidify:

* A **private note** is generated, containing two random values: a **secret** and a **nullifier**.
* These values are hashed together using the **Poseidon** hash function, creating a **commitment**.
* This commitment is added as a leaf to a Merkle tree stored on-chain.
* The user must store the private note securely, as it will be required to withdraw later.

***

#### **How Withdrawals Work**

To withdraw from the pool:

* The user generates a **zk-proof** that they know a valid, unused commitment in the Merkle tree.
* A **nullifier hash** is submitted, ensuring the commitment cannot be spent twice.
* The smart contract verifies the zk-proof and nullifier.
* If valid, the contract releases the funds to the recipient address.

Since the proof reveals no information about the original commitment’s position in the Merkle tree, and the nullifier cannot be linked back to the deposit, the source of funds remains private.

***

#### **Zero-Knowledge Proofs (zk-Proofs)**

Voidify uses **zk-SNARKs** — succinct, non-interactive cryptographic proofs that verify claims without revealing the underlying data.

* **Privacy**: Proves ownership of a deposit without revealing which one.
* **Security**: Prevents double-spending through nullifier tracking.
* **Efficiency**: Proofs are generated off-chain and verified on-chain.

***

#### ⚙**Poseidon Hash: Optimized for zk-Proofs on Solana**

Voidify uses the **Poseidon hash** instead of older hash functions like Pedersen. This switch dramatically improves performance on Solana:

| Feature                | Pedersen Hash        | Poseidon Hash        |
| ---------------------- | -------------------- | -------------------- |
| zk-Proof Efficiency    | High constraint cost | Minimal constraints  |
| Compatibility          | EVM-optimized        | zk-circuit optimized |
| Cost & Latency         | Expensive            | Fast & cheap         |
| Suitability for Solana | Poor                 | Excellent            |

**Why Poseidon Hash Matters:**

* Reduced computation = faster proof generation
* Optimized for Solana’s low-latency execution
* Lower contract execution cost
* Maintains strong zk-security guarantees

***

#### **Privacy Tips**

To enhance your privacy:

* Use **relayers** to hide your withdrawal origin
* Wait for additional deposits before withdrawing to increase your anonymity set
* Never reuse notes or expose secret values
* Consider different gas parameters and timing for transactions

***

#### **Summary**

Voidify allows you to transact privately on Solana by combining:

* Zero-knowledge cryptography (zk-SNARKs)
* ZK-optimized hashing (Poseidon)
* High-speed, low-cost smart contracts
* A fully self-custodial architecture

The protocol empowers users to move assets without revealing their activity — giving them privacy without compromising security or decentralization.

***

## 中文

### 匿名池

Voidify 使用固定面额的隐私池，例如 `0.1 SOL`、`1 SOL` 或 `10 SOL`。用户存入某个池子后会获得一份私密 note，之后可通过零知识证明将相同金额提取到另一个钱包。该证明只表明用户拥有一笔有效且未使用的存款，不会显示具体是哪一笔。

同一个池中的独立存款越多，每次提款可能对应的来源越多。时间也很重要：存入后立即提款更容易被关联；等待池中出现更多活动通常能增强实际隐私。

### 存款与提款

存款时：

* 浏览器生成包含 secret 和 nullifier 的私密 note。
* Poseidon 将这些值哈希为 commitment。
* Commitment 被加入链上的 Merkle 树。
* 用户必须安全保存 note，以便之后提款。

提款时：

* 用户生成证明其拥有有效且未使用 commitment 的 zk-proof。
* Nullifier hash 防止同一 note 被重复使用。
* 程序验证证明后将资金发送至收款地址。

证明不会公开正在使用的是 Merkle 树中的哪一个叶子，因此存款与提款不会在链上被直接关联。

### 密码学与隐私建议

Voidify 使用 zk-SNARKs 生成紧凑证明，并使用适合零知识电路高效计算的 Poseidon 哈希函数。

为了提高隐私：

* 通过 relayer 提款。
* 在提款前等待同一池中出现更多存款。
* 绝不要分享或重复使用私密 note。
* 避免明显的操作时间规律或钱包复用。

***

## Русский

### Пулы анонимности

Voidify использует пулы приватности фиксированного номинала, например `0.1 SOL`, `1 SOL` или `10 SOL`. Пользователь вносит средства в один пул и получает приватную note. Позднее он может вывести ту же сумму на другой кошелек с доказательством нулевого разглашения, подтверждающим владение одним действительным неиспользованным депозитом без раскрытия конкретного депозита.

Чем больше независимых депозитов в пуле, тем больше возможных источников имеет каждый вывод. Важен и момент вывода: немедленный вывод после внесения проще сопоставить, тогда как ожидание дополнительной активности обычно улучшает практическую приватность.

### Депозиты и выводы

При внесении:

* Браузер создает приватную note, содержащую secret и nullifier.
* Poseidon хеширует эти значения в commitment.
* Commitment добавляется в ончейн-дерево Merkle.
* Пользователь должен надежно сохранить note для последующего вывода.

При выводе:

* Пользователь генерирует zk-proof действительного неиспользованного commitment.
* Nullifier hash предотвращает повторное расходование одной note.
* Программа проверяет доказательство и отправляет средства получателю.

Доказательство не раскрывает, какой лист дерева Merkle расходуется, поэтому депозит и вывод не связываются напрямую в блокчейне.

### Криптография и рекомендации по приватности

Voidify использует zk-SNARKs для компактных доказательств и хеш-функцию Poseidon, эффективную внутри схем нулевого разглашения.

Для улучшения приватности:

* Выводите средства через relayer.
* Ждите новых депозитов в том же пуле перед выводом.
* Никогда не передавайте и не используйте повторно приватную note.
* Избегайте узнаваемых временных шаблонов и повторного использования кошельков.

***

## 日本語

### 匿名性プール

Voidify は `0.1 SOL`、`1 SOL`、`10 SOL` などの固定額プライバシープールを使用します。ユーザーは一つのプールに預け入れて秘密の note を受け取り、後からゼロ知識証明により同額を別のウォレットへ出金できます。この証明は、有効で未使用の預入を所有していることだけを示し、どの預入かは明かしません。

同じプール内の独立した預入が多いほど、各出金に対する候補の出所が増えます。タイミングも重要で、預入直後の出金は関連付けやすく、追加のプール活動を待つことは通常、実用上のプライバシーを高めます。

### 預入と出金

預入時：

* ブラウザが secret と nullifier を含む秘密の note を生成します。
* Poseidon がそれらを commitment にハッシュします。
* Commitment がオンチェーンの Merkle tree に追加されます。
* ユーザーは出金に備えて note を安全に保管する必要があります。

出金時：

* ユーザーが有効で未使用の commitment を持つことを示す zk-proof を生成します。
* Nullifier hash が同じ note の二重使用を防ぎます。
* プログラムが証明を検証し、受取アドレスへ資金を送ります。

証明は Merkle tree のどの葉が使用されるかを公開しないため、預入と出金はオンチェーンで直接結び付きません。

### 暗号技術とプライバシーのヒント

Voidify は簡潔な証明のために zk-SNARKs を使用し、ゼロ知識回路内で効率的な Poseidon ハッシュ関数を採用しています。

プライバシーを高めるには：

* Relayer を通じて出金します。
* 同じプールに追加の預入が入るまで待ってから出金します。
* 秘密の note を共有したり再利用したりしないでください。
* 特徴的なタイミングやウォレットの再利用を避けてください。
