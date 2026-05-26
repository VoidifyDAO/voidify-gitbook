---
description: How Voidify Works
---

# II. The Mechanism: Breaking the Link

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2FMDD8YhvhqGpVn2jmw9pd%2Fvoidify%20astronaut.png?alt=media&#x26;token=f48c2cea-4c25-4fed-98af-29b956398485" alt="" width="275"><figcaption></figcaption></figure>

***

## English

### Anonymity Pools

Voidify uses fixed-denomination privacy pools, such as `0.1 SOL`, `1 SOL`, or `10 SOL`. A user deposits into one pool and receives a private note. Later, the user can withdraw the same amount to a different wallet with a zero-knowledge proof that shows ownership of one valid, unused deposit without identifying it.

A pool with more independent deposits gives each withdrawal more plausible sources. Timing matters as well: withdrawing immediately after depositing can make correlation easier, while waiting for additional pool activity usually improves practical privacy.

### Deposits and Withdrawals

When depositing:

* The browser generates a private note containing a secret and a nullifier.
* Poseidon hashes those values into a commitment.
* The commitment is added to an on-chain Merkle tree.
* The user must securely preserve the note for withdrawal.

When withdrawing:

* The user generates a zk-proof of a valid unused commitment.
* A nullifier hash prevents the same note from being spent twice.
* The program verifies the proof and sends funds to the recipient.

The proof does not reveal which Merkle tree leaf is being spent, so the deposit and withdrawal are not directly linked on-chain.

### Cryptography and Privacy Tips

Voidify uses zk-SNARKs for compact proofs and the Poseidon hash function because it is efficient inside zero-knowledge circuits.

To improve privacy:

* Withdraw through a relayer.
* Wait for more deposits in the same pool before withdrawing.
* Never share or reuse a private note.
* Avoid recognizable timing or wallet-reuse patterns.

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
