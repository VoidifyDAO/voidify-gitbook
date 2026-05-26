# IX. Trust Setup

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

### Why a Ceremony Is Required

Voidify withdrawals use Groth16 proofs verified on-chain against a fixed verifying key. Generating that key requires secret randomness. If one party kept all of that randomness, it could forge valid-looking proofs. A multi-party setup ceremony is designed so that the keys remain sound if at least one contributor behaves honestly and deletes their entropy.

Phase 1 uses a public Powers of Tau transcript. Phase 2 is specific to Voidify's withdrawal circuit and produces the final proving and verifying keys for that circuit.

### Contributing

In the ceremony application, a contributor connects a wallet, provides fresh entropy, and submits a contribution. The cryptographic computation occurs in the browser, and the secret entropy does not need to leave the contributor's device.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Verifiability

The ceremony is designed for public verification:

* Each contribution must extend the previous transcript.
* The transcript and contribution records can be published for independent auditing.
* The frontend can be built reproducibly and pinned to IPFS.
* After contributions close, a public-beacon randomness layer can be added before extracting the final verifying key.

The resulting key is secure under the central ceremony assumption: at least one contributor honestly discards their secret entropy.

***

## 中文

### 为什么需要仪式

Voidify 提款使用 Groth16 证明，并在链上通过固定 verifying key 进行验证。生成该密钥需要秘密随机数。如果某一方保留了全部随机数，就可能伪造看似有效的证明。多方可信设置仪式的目标是：只要至少一位参与者诚实地操作并删除其熵，最终密钥就保持可靠。

Phase 1 使用公开的 Powers of Tau 记录。Phase 2 专门对应 Voidify 的提款电路，并生成该电路最终使用的 proving key 与 verifying key。

### 参与贡献

在仪式应用中，参与者连接钱包、提供新的熵并提交贡献。关键密码学计算在浏览器中完成，秘密熵无需离开参与者的设备。

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### 可验证性

该仪式面向公开验证设计：

* 每一份贡献都必须延续上一份 transcript。
* Transcript 与贡献记录可以公开，以供独立审计。
* 前端可进行可复现构建并固定在 IPFS 上。
* 贡献结束后，可在提取最终 verifying key 前加入公共 beacon 随机层。

最终密钥的安全性依赖于仪式的核心假设：至少有一位参与者诚实地删除了自己的秘密熵。

***

## Русский

### Зачем нужна церемония

Выводы Voidify используют доказательства Groth16, проверяемые ончейн по фиксированному verifying key. Для создания этого ключа требуется секретная случайность. Если одна сторона сохранит всю эту случайность, она сможет подделывать доказательства, выглядящие действительными. Многосторонняя церемония настройки устроена так, чтобы ключи оставались надежными, если хотя бы один участник действовал честно и удалил свою энтропию.

Phase 1 использует публичный транскрипт Powers of Tau. Phase 2 относится именно к схеме вывода Voidify и создает окончательные proving key и verifying key для этой схемы.

### Участие

В приложении церемонии участник подключает кошелек, предоставляет новую энтропию и отправляет вклад. Криптографическое вычисление происходит в браузере, а секретная энтропия не должна покидать устройство участника.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### Проверяемость

Церемония проектируется для публичной проверки:

* Каждый вклад должен продолжать предыдущий транскрипт.
* Транскрипт и записи вкладов могут публиковаться для независимого аудита.
* Фронтенд может воспроизводимо собираться и закрепляться в IPFS.
* После завершения вкладов перед извлечением окончательного verifying key может быть добавлен публичный beacon-слой случайности.

Полученный ключ безопасен при центральном допущении церемонии: хотя бы один участник честно удалил свою секретную энтропию.

***

## 日本語

### なぜセレモニーが必要か

Voidify の出金は、固定された verifying key に対してオンチェーンで検証される Groth16 証明を使用します。このキーの生成には秘密の乱数が必要です。一者がすべての乱数を保持していれば、有効に見える証明を偽造できる可能性があります。マルチパーティのセットアップセレモニーは、少なくとも一人の参加者が誠実に行動し、自身のエントロピーを削除すれば、キーの健全性が保たれるよう設計されています。

Phase 1 は公開された Powers of Tau transcript を使用します。Phase 2 は Voidify の出金回路に固有であり、その回路用の最終 proving key と verifying key を生成します。

### 貢献方法

セレモニーアプリケーションで、参加者はウォレットを接続し、新しいエントロピーを提供して貢献を送信します。暗号学的計算はブラウザ内で行われ、秘密のエントロピーを参加者のデバイス外へ送る必要はありません。

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### 検証可能性

セレモニーは公開検証を可能にするよう設計されています。

* 各貢献は前の transcript を延長する必要があります。
* Transcript と貢献記録は独立監査のために公開できます。
* フロントエンドは再現可能にビルドし、IPFS に固定できます。
* 貢献終了後、最終 verifying key の抽出前に公開 beacon の乱数層を追加できます。

生成されたキーの安全性は、少なくとも一人の参加者が秘密のエントロピーを誠実に破棄したというセレモニーの中心的な仮定に基づきます。
