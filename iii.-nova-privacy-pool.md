---
description: Flexible private deposits and withdrawals with Voidify Nova
---

# III. Nova Privacy Pool

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

Nova is Voidify's flexible-amount privacy pool. Unlike Classic pools, which use fixed denominations, Nova lets a user deposit an amount they choose and later withdraw all or part of the resulting private balance.

Nova remains non-custodial. The user's browser generates the zero-knowledge proof, the Solana program verifies it, and a nullifier prevents the same private state from being spent twice. Neither Voidify nor a relayer can spend a user's Nova balance without the key derived by that user.

#### Nova and Classic

| | Classic | Nova |
| --- | --- | --- |
| Amounts | Fixed denominations | Flexible amounts within the pool's limits |
| Private state | A separate private note for each deposit | An encrypted balance replaced after each deposit or withdrawal |
| Partial withdrawal | No | Yes |
| Access | Saved private note | Wallet signature and optional passphrase |
| Waiting pressure | Privacy grows inside one denomination, so rare or large denominations may take longer to gain peers | No need to wait for another deposit of the exact same amount; activity across the token's Nova pool contributes to the private state set |
| Best suited for | Standardized deposits and a denomination-based anonymity set | Flexible deposits, balance top-ups, and partial withdrawals |

Both modes use zero-knowledge proofs to break the public link between the source of funds and the recipient. Flexible amounts improve usability, but unusual amounts and distinctive timing can still create correlation clues. Cryptography does not remove metadata risk.

#### Why Nova Usually Requires Less Waiting

Classic privacy is divided by denomination. A 100 SOL Classic deposit benefits mainly from other deposits in the same 100 SOL pool, so a rare or large denomination may require waiting for another matching deposit before its anonymity set grows.

Nova removes that exact-denomination bottleneck:

* There is no protocol-enforced waiting period.
* A large deposit does not need another deposit of exactly the same size to become part of a broader private state set.
* Deposits of different sizes create encrypted commitments in the same token pool.
* A user can withdraw part of a balance and leave the remainder private instead of waiting for a matching fixed-denomination withdrawal path.
* Balance top-ups and partial withdrawals make it harder to model every action as a simple one-deposit-to-one-withdrawal pair.

This means users generally do not need to wait merely for an identical amount to appear. Waiting can still improve privacy in a quiet pool, and an immediate withdrawal of a distinctive public amount may remain easy to correlate. Nova reduces the denomination-driven wait; it does not make timing irrelevant.

#### How a Nova Balance Works

Nova represents a user's private balance as an encrypted output committed to an on-chain Merkle tree.

* On the first deposit, Nova creates a new private output.
* On a later deposit, Nova spends the user's current output and creates a replacement containing the old balance plus the new amount.
* On a withdrawal, Nova spends the current output, sends the requested amount minus applicable fees to the recipient, and creates a replacement output containing the remaining private balance.
* The proof confirms that the input exists, belongs to the user, has not been spent, and that the value transition is valid—without revealing which commitment is being consumed.

Only the latest unspent output is the active Nova balance for a particular wallet, passphrase, and token.

#### Unlocking the Nova Key

Before Nova can find or update a balance, the interface asks the connected wallet to sign the message **“Voidify Nova account sign in.”** This is an off-chain signature: it does not submit a Solana transaction and does not spend SOL.

The signature is used locally to derive the encryption identity that can discover and decrypt the user's Nova outputs. The key is scoped to the connected wallet.

An optional passphrase can be included in key derivation:

* The same wallet with different passphrases opens different Nova balances.
* The passphrase is case-sensitive; spaces and punctuation matter.
* Voidify cannot recover a forgotten passphrase.
* A wrong passphrase usually appears as an empty or different balance—it does not reset the original balance.

{% hint style="warning" %}
Never sign the Nova unlock message on an untrusted website. Verify the domain and the exact wallet prompt before approving it. A passphrase is not a substitute for wallet security.
{% endhint %}

#### Deposit with Nova

1. Open **Nova** and connect a supported Solana wallet.
2. Select an available token. The assets shown in the interface depend on the active deployment.
3. Unlock the Nova key, using the same passphrase you intend to use for this balance.
4. Enter a positive amount that respects the token's decimal precision and the pool's current on-chain limits.
5. Review the token, amount, and passphrase status, then approve the deposit transaction.
6. Wait for Nova to synchronize commitments and generate the proof. After confirmation, the displayed private balance includes the new deposit.

Proof generation happens on the user's device and can take longer than an ordinary Solana transfer. Do not close the page or switch wallets while a proof is being generated.

#### Withdraw with Nova

1. Connect the wallet used to derive the Nova key.
2. Unlock Nova with the original passphrase, if one was used.
3. Select the token and wait for the private balance to synchronize.
4. Enter a withdrawal amount no greater than the available Nova balance, then enter the recipient address.
5. Review the selected relayer and the fee summary.
6. Confirm the withdrawal. The browser generates the proof and sends the prepared request to the relayer for submission.

The requested withdrawal amount includes the relayer and treasury fees shown in the confirmation summary. The recipient receives the amount remaining after those fees. Any unwithdrawn value stays private in a newly created Nova output.

For SPL tokens, the recipient may need an associated token account. Creating a missing account can require a normal Solana transaction from the connected wallet.

#### Privacy and Recovery Checklist

* Use the same wallet and exact passphrase to recover a Nova balance on another trusted device.
* Lock the Nova key and clear site data on shared devices. Clearing local data does not destroy the on-chain balance, but you will need the wallet and passphrase to derive it again.
* Do not treat the displayed balance as final until the transaction is confirmed.
* Avoid unique amounts and immediate deposit-to-withdraw patterns when stronger practical privacy is important.
* Check the recipient, token, amount, relayer, and fees before confirming. Blockchain transactions are irreversible.
* Never share serialized notes, derived keys, wallet signatures, seed phrases, or passphrases.

Nova protects the on-chain relationship between private state transitions. Wallet reuse, IP addresses, RPC logs, browser fingerprints, timing, and exchange records can still reveal information. See [Stay Shadowed](xi.-stay-shadowed.md) for operational privacy guidance.

***

## 中文

Nova 是 Voidify 的灵活金额隐私池。与采用固定面额的 Classic 池不同，Nova 允许用户自行选择存款金额，并在之后提取全部或部分私密余额。

Nova 仍然是非托管的。用户浏览器生成零知识证明，Solana 程序负责验证，nullifier 防止同一份私密状态被重复花费。没有用户自己派生的密钥，Voidify 或 relayer 都无法支配用户的 Nova 余额。

#### Nova 与 Classic

| | Classic | Nova |
| --- | --- | --- |
| 金额 | 固定面额 | 在池的限制范围内灵活选择金额 |
| 私密状态 | 每笔存款对应一份独立 private note | 每次存款或提款后都会替换的一份加密余额 |
| 部分提款 | 不支持 | 支持 |
| 访问方式 | 保存的 private note | 钱包签名和可选 passphrase |
| 等待压力 | 隐私在单一面额池内增长，冷门或大额面额可能需要更久才能等到同类存款 | 不需要等待另一笔完全相同金额的存款；同一代币 Nova 池内的活动共同构成私密状态集合 |
| 更适合 | 标准化存款及基于面额的 anonymity set | 灵活存款、追加余额和部分提款 |

两种模式都使用零知识证明打破资金来源与收款人之间的公开链上联系。灵活金额提升了易用性，但独特金额和明显的时间模式仍可能形成关联线索。密码学无法消除元数据风险。

#### 为什么 Nova 通常不需要等待太久

Classic 的隐私按面额分开。比如一笔 100 SOL 的 Classic 存款，主要依赖同一个 100 SOL 池中的其他存款来扩大匿名集。因此，冷门或大额面额可能需要等待另一笔相同面额的存款出现。

Nova 消除了这种“必须匹配面额”的瓶颈：

* 协议没有强制等待期。
* 大额存款不需要等待另一笔完全相同金额的大额存款，才能进入更广泛的私密状态集合。
* 不同金额的存款会在同一代币的 Nova 池中创建加密 commitments。
* 用户可以只提取部分余额，让剩余资金继续保持私密，不必寻找对应的固定面额提款路径。
* 追加余额和部分提款使外部观察者更难把每次操作简化为“一笔存款对应一笔提款”。

因此，用户通常不需要仅仅为了等待相同金额出现而长时间停留。但在低活跃池中，适当拉开时间仍能改善隐私；如果立即提取一个非常独特的公开金额，仍可能形成关联线索。Nova 减少的是面额造成的等待，并不代表时间因素完全失效。

#### Nova 余额如何工作

Nova 将用户的私密余额表示为一个加密输出，并把对应 commitment 加入链上 Merkle tree。

* 第一次存款时，Nova 创建一个新的私密输出。
* 后续存款时，Nova 花费用户当前的输出，并创建一个包含“原余额 + 新存款”的替代输出。
* 提款时，Nova 花费当前输出，将请求金额扣除适用费用后发送给收款人，并创建一个包含剩余私密余额的替代输出。
* 零知识证明会确认输入真实存在、属于用户、尚未被花费，而且金额转换有效，但不会暴露具体消费了哪一个 commitment。

对于特定的钱包、passphrase 和代币，只有最新且未花费的输出才是当前有效的 Nova 余额。

#### 解锁 Nova 密钥

Nova 在查找或更新余额之前，会请求已连接的钱包签名 **“Voidify Nova account sign in”**。这是链下签名，不会提交 Solana 交易，也不会消耗 SOL。

该签名会在本地用于派生加密身份，以发现并解密属于用户的 Nova 输出。派生的密钥与当前连接的钱包绑定。

用户还可以选择在密钥派生中加入 passphrase：

* 同一个钱包使用不同 passphrase，会打开不同的 Nova 余额。
* Passphrase 区分大小写，空格和标点也会影响结果。
* Voidify 无法找回遗忘的 passphrase。
* 输入错误 passphrase 通常只会显示为空余额或另一份余额，不会重置原来的余额。

{% hint style="warning" %}
不要在不可信的网站上签署 Nova 解锁消息。批准前请核对域名和钱包显示的完整签名内容。Passphrase 不能替代钱包本身的安全保护。
{% endhint %}

#### 使用 Nova 存款

1. 打开 **Nova**，连接兼容的 Solana 钱包。
2. 选择当前可用的代币；界面显示的资产取决于当前部署。
3. 解锁 Nova 密钥，并使用你之后准备继续访问这份余额的同一个 passphrase。
4. 输入大于零、符合代币精度并处于当前链上池限制范围内的金额。
5. 核对代币、金额和 passphrase 状态，然后批准存款交易。
6. 等待 Nova 同步 commitments 并生成证明。交易确认后，显示的私密余额会包含本次存款。

证明在用户设备上生成，耗时可能长于普通 Solana 转账。生成证明期间不要关闭页面或切换钱包。

#### 使用 Nova 提款

1. 连接派生 Nova 密钥时使用的钱包。
2. 如果之前设置过 passphrase，请使用完全相同的内容解锁 Nova。
3. 选择代币并等待私密余额同步完成。
4. 输入不超过可用 Nova 余额的提款金额，再填写收款地址。
5. 核对选中的 relayer 和费用摘要。
6. 确认提款。浏览器生成证明，并把准备好的请求发送给 relayer 提交。

请求的提款金额包含确认摘要中显示的 relayer fee 和 treasury fee，收款人获得扣除这些费用后的金额。未提取的价值会保留在新创建的 Nova 私密输出中。

对于 SPL 代币，收款人可能需要 associated token account。如果该账户不存在，创建账户可能需要由当前连接的钱包发起一笔普通 Solana 交易。

#### 隐私与恢复检查清单

* 在另一台可信设备上恢复 Nova 余额时，使用同一个钱包和完全一致的 passphrase。
* 在共享设备上使用后锁定 Nova 密钥并清理站点数据。清理本地数据不会销毁链上余额，但之后需要钱包和 passphrase 重新派生密钥。
* 交易确认前，不要把界面显示的余额视为最终结果。
* 如果需要更强的实际隐私，应避免独特金额以及存款后立即提款的模式。
* 确认前核对收款人、代币、金额、relayer 和费用。区块链交易不可逆。
* 永远不要分享序列化 note、派生密钥、钱包签名、助记词、seed phrase 或 passphrase。

Nova 保护的是私密状态转换之间的链上关系。钱包复用、IP 地址、RPC 日志、浏览器指纹、操作时间和交易所记录仍可能泄露信息。更多操作层面的隐私建议请参阅 [Stay Shadowed](xi.-stay-shadowed.md)。

***

## Русский

Nova — это privacy pool Voidify с гибкими суммами. В отличие от Classic pools с фиксированными номиналами, Nova позволяет выбрать сумму депозита и позднее вывести весь приватный баланс или его часть.

Nova остается некастодиальной. Браузер пользователя создает zero-knowledge proof, программа Solana проверяет его, а nullifier не позволяет потратить одно и то же приватное состояние дважды. Ни Voidify, ни relayer не могут распорядиться балансом Nova без ключа, полученного самим пользователем.

#### Nova и Classic

| | Classic | Nova |
| --- | --- | --- |
| Суммы | Фиксированные номиналы | Гибкие суммы в пределах ограничений pool |
| Приватное состояние | Отдельная private note для каждого депозита | Зашифрованный баланс, заменяемый после каждого депозита или вывода |
| Частичный вывод | Нет | Да |
| Доступ | Сохраненная private note | Подпись wallet и опциональная passphrase |
| Ожидание | Privacy растет внутри одного номинала, поэтому редкие или крупные номиналы могут дольше ждать похожих депозитов | Не нужно ждать депозит точно такого же размера; активность всего Nova pool данного token участвует в private state set |
| Лучше подходит для | Стандартизированных депозитов и anonymity set по номиналу | Гибких депозитов, пополнения баланса и частичных выводов |

Оба режима используют zero-knowledge proofs, чтобы разорвать публичную ончейн-связь между источником средств и получателем. Гибкие суммы удобнее, но необычные суммы и характерный timing все равно могут создавать подсказки для корреляции. Криптография не устраняет риск метаданных.

#### Почему Nova обычно требует меньше ожидания

В Classic privacy разделена по номиналам. Крупный или редко используемый номинал получает больше anonymity только после появления других депозитов в том же fixed-denomination pool.

Nova устраняет необходимость точного совпадения суммы:

* Протокол не устанавливает обязательный период ожидания.
* Крупному депозиту не нужен другой депозит точно такого же размера.
* Депозиты разных размеров создают encrypted commitments в одном Nova pool для выбранного token.
* Можно вывести часть баланса, оставив остаток приватным.
* Пополнения и частичные выводы усложняют модель «один депозит — один вывод».

Поэтому ждать только ради появления идентичной суммы обычно не требуется. В тихом pool дополнительная активность и временной интервал все равно могут улучшить privacy, а немедленный вывод уникальной публичной суммы может быть сопоставлен. Nova уменьшает ожидание, вызванное номиналами, но не отменяет значение timing.

#### Как работает баланс Nova

Nova представляет приватный баланс пользователя как зашифрованный output, commitment которого добавляется в ончейн Merkle tree.

* При первом депозите Nova создает новый приватный output.
* При следующем депозите Nova тратит текущий output и создает замену с прежним балансом плюс новая сумма.
* При выводе Nova тратит текущий output, отправляет получателю запрошенную сумму за вычетом fees и создает замену с оставшимся приватным балансом.
* Proof подтверждает существование и принадлежность input, отсутствие double-spend и корректность перехода суммы, не раскрывая использованный commitment.

Для конкретной комбинации wallet, passphrase и token активным является только самый новый непотраченный output.

#### Разблокировка ключа Nova

Перед поиском или обновлением баланса интерфейс просит wallet подписать **“Voidify Nova account sign in.”** Это off-chain подпись: она не отправляет транзакцию Solana и не расходует SOL. Подпись локально используется для получения encryption identity, способной находить и расшифровывать Nova outputs пользователя.

При получении ключа можно добавить passphrase:

* Один wallet с разными passphrases открывает разные балансы Nova.
* Passphrase чувствительна к регистру; пробелы и знаки препинания имеют значение.
* Voidify не может восстановить забытую passphrase.
* Неверная passphrase обычно выглядит как пустой или другой баланс и не сбрасывает исходный баланс.

{% hint style="warning" %}
Не подписывайте сообщение разблокировки Nova на недоверенном сайте. Перед подтверждением проверьте домен и точный текст в wallet. Passphrase не заменяет безопасность wallet.
{% endhint %}

#### Депозит и вывод

1. Откройте **Nova**, подключите Solana wallet и выберите доступный token.
2. Разблокируйте ключ Nova с нужной passphrase.
3. Для депозита введите положительную сумму в пределах ончейн-ограничений pool и подтвердите транзакцию.
4. Для вывода дождитесь синхронизации, введите сумму не больше доступного баланса и адрес получателя.
5. Проверьте relayer и fees, затем подтвердите. Browser создаст proof и отправит запрос relayer.

Получатель получает запрошенную сумму за вычетом relayer fee и treasury fee. Невыведенная часть остается приватной в новом output. Proof создается на устройстве и может занять больше времени, чем обычный перевод Solana.

#### Приватность и восстановление

* Для восстановления используйте тот же wallet и точную passphrase.
* На общем устройстве блокируйте Nova key и очищайте site data.
* Избегайте уникальных сумм и немедленного вывода после депозита.
* Перед подтверждением проверяйте recipient, token, amount, relayer и fees.
* Никогда не передавайте notes, derived keys, wallet signatures, seed phrases или passphrases.

Nova защищает ончейн-связь между переходами private state. IP-адреса, RPC logs, browser fingerprints, timing и exchange records все еще могут раскрывать информацию. См. [Stay Shadowed](xi.-stay-shadowed.md).

***

## 日本語

Nova は、Voidify の柔軟な金額に対応した privacy pool です。固定額を使う Classic pool とは異なり、ユーザーは任意の金額を deposit し、その private balance の全部または一部を後から withdraw できます。

Nova は non-custodial です。Browser が zero-knowledge proof を生成し、Solana program が検証し、nullifier が同じ private state の二重使用を防ぎます。ユーザーが導出した key がなければ、Voidify も relayer も Nova balance を使用できません。

#### Nova と Classic

| | Classic | Nova |
| --- | --- | --- |
| 金額 | 固定額 | Pool の制限内で柔軟な金額 |
| Private state | Deposit ごとの private note | Deposit / withdraw ごとに置き換えられる encrypted balance |
| 一部出金 | 不可 | 可能 |
| Access | 保存した private note | Wallet signature と任意の passphrase |
| 待機負担 | Privacy は 1 つの額面内で増えるため、希少または大口の額面は同額 deposit を長く待つ場合がある | 完全に同じ金額の deposit を待つ必要がなく、同じ token の Nova pool 全体の activity が private state set に加わる |
| 適した用途 | 標準化された deposit と額面ごとの anonymity set | 柔軟な deposit、残高追加、一部 withdraw |

どちらも zero-knowledge proof により、資金元と recipient の公開オンチェーン上のリンクを切断します。ただし、特徴的な金額や timing は相関の手掛かりになり得ます。

#### Nova で待機時間を短くできる理由

Classic の privacy は額面ごとに分かれます。大口または利用の少ない額面では、同じ fixed-denomination pool に別の deposit が入るまで anonymity set が増えにくい場合があります。

Nova は金額の完全一致という制約を取り除きます。

* Protocol が強制する待機期間はありません。
* 大口 deposit でも、完全に同じ金額の別 deposit を待つ必要はありません。
* 異なる金額の deposits が、同じ token の Nova pool に encrypted commitments を作ります。
* Balance の一部だけを withdraw し、残りを private に保てます。
* Top-up と partial withdrawal により、「1 deposit 対 1 withdrawal」という単純な対応付けが難しくなります。

そのため、同額の出現だけを目的に長時間待つ必要は通常ありません。ただし activity の少ない pool では時間を空けることが privacy 改善につながり、特徴的な公開金額を即時 withdraw すると相関される可能性があります。Nova は額面による待機を減らしますが、timing を無関係にはしません。

#### Nova Balance の仕組み

Nova は private balance を encrypted output として表し、その commitment をオンチェーン Merkle tree に追加します。

* 最初の deposit で新しい private output を作成します。
* 追加 deposit では現在の output を使い、旧残高と新しい金額を合計した replacement output を作成します。
* Withdraw では現在の output を使い、fees を差し引いた要求額を recipient へ送り、残高を持つ replacement output を作成します。
* Proof は input の存在、所有、未使用、value transition の正しさを確認しますが、使用した commitment は明かしません。

特定の wallet、passphrase、token では、最新の未使用 output だけが active Nova balance です。

#### Nova Key の Unlock

Balance を検索または更新する前に、wallet は **“Voidify Nova account sign in”** への署名を求められます。これは off-chain signature で、Solana transaction を送信せず SOL も消費しません。Signature は Nova outputs を発見して復号する encryption identity の導出にローカルで使われます。

任意の passphrase を追加できます。

* 同じ wallet でも異なる passphrase は別々の Nova balance を開きます。
* 大文字小文字、空白、記号はすべて結果に影響します。
* Voidify は忘れた passphrase を復元できません。
* 間違った passphrase は通常、空または別の balance として表示されます。

{% hint style="warning" %}
信頼できないサイトで Nova unlock message に署名しないでください。承認前に domain と wallet prompt を確認してください。
{% endhint %}

#### Deposit と Withdraw

1. **Nova** を開き、Solana wallet を接続して利用可能な token を選びます。
2. 使用する passphrase で Nova key を unlock します。
3. Deposit では、オンチェーン pool limits 内の正の金額を入力して transaction を承認します。
4. Withdraw では同期完了を待ち、利用可能 balance 以下の金額と recipient address を入力します。
5. Relayer と fees を確認して承認します。Browser が proof を生成し、request を relayer に送信します。

Recipient は要求額から relayer fee と treasury fee を差し引いた金額を受け取ります。残りは新しい private output に保持されます。Proof generation は通常の Solana transfer より時間がかかる場合があります。

#### Privacy と Recovery

* 復元には同じ wallet と完全に同じ passphrase を使います。
* 共有 device では Nova key を lock し、site data を消去します。
* 特徴的な金額や deposit 直後の withdraw を避けます。
* Confirm 前に recipient、token、amount、relayer、fees を確認します。
* Notes、derived keys、wallet signatures、seed phrases、passphrases を共有しないでください。

Nova が保護するのは private state transitions 間のオンチェーン関係です。IP address、RPC logs、browser fingerprint、timing、exchange records は情報を漏らす可能性があります。[Stay Shadowed](xi.-stay-shadowed.md) も参照してください。
