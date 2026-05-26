---
description: How to Deposit & Withdraw Using Voidify
---

# IV. Deposit & Withdraw

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

Voidify allows users to deposit fixed-denomination assets into privacy pools and later withdraw them with zero-knowledge proofs. This process creates unlinkability between addresses — but users must follow best practices to preserve their privacy.

#### **Deposit Guide**

**1. Connect Your Wallet**

Click **Connect** and choose a Solana-compatible wallet such as:

* ✅ Phantom
* ✅ Solflare
* ✅ Metamask

Ensure you're connected to **Solana Mainnet**.

***

**2. Select a Token & Amount**

Choose the token you want to deposit (**SOL**) and the corresponding **fixed-denomination pool** (e.g., 1 SOL, 10 SOL,).

{% hint style="info" %}
Standardized pool sizes help protect privacy by eliminating unique transaction fingerprints.
{% endhint %}

***

**3. Generate and Secure Your Note**

Click deposit:

* A **private note** will be generated in your browser.
* This note proves you deposited — and is required to withdraw later.

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

> ⚠️ **Important**: Save your note securely.\
> Voidify does not store it. If you lose it, your funds are irrecoverable.

**Do not store notes in:**

* Unencrypted devices
* Browsers or autofill
* Cloud storage or chat apps

***

**4. Confirm Deposit**

Once you've saved the note:

* Click **Confirm**
* Approve the transaction in your wallet
* Your funds will be added to the on-chain privacy pool

***

**5. Wait to Strengthen Privacy**

Withdrawing immediately weakens your anonymity.\
To increase your privacy:

* Wait for more users to deposit into the same pool
* Larger **anonymity sets** reduce correlation risk

You’ll be able to monitor pool activity in the **Anonymity Set Dashboard**.

***

#### **Withdraw Guide**

**1. Connect Wallet & Select Pool**\
Click **Connect** → Choose your wallet → Navigate to the **Withdraw** tab.

***

**2. Paste Your Private Note and Recipient Address**\
Paste your saved note and recipient address into the withdrawal field.

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

> This cryptographically proves you made a deposit — without revealing which one.

***

**3. Choose a Relayer (opeitonal, Because the system will automatically choose)**&#x20;

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

* Select a **relayer** to submit the withdrawal transaction on your behalf

***

**4. Click Withdraw**

* **Click Withdraw**
* Click **Confirm**

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

> The funds will be sent to your selected address without any visible on-chain link to your deposit.

***

**Optional: Note Account (Coming Soon)**

Voidify is building a secure **on-chain backup feature** called the **Note Account**.\
This will allow you to store encrypted notes without relying on off-chain tools.

> ⚠️ Use caution: if your backup key is ever compromised, your deposits can be deanonymized.\
> Only use this feature if you fully understand the tradeoffs.

***

**Never Share Your Note**

Your private note is your key to withdraw funds.\
If anyone accesses it, they can withdraw your deposit.

* ❌ Don’t screenshot it
* ❌ Don’t store in cloud apps
* ❌ Don’t paste in browsers or shared devices

> Losing your note = permanent loss of access.

***

#### Summary

* Use a supported Solana wallet
* Choose a fixed pool size
* Save your private note securely
* Wait for other users to deposit before withdrawing
* Use a relayer to protect your withdrawal identity
* Never reuse wallets
* Never share your private note

Voidify gives you cryptographic privacy.\
Protecting it is your responsibility.

***

## 中文

Voidify 允许用户将固定面额的资产存入隐私池，之后通过零知识证明提款。Note 的保存方式、钱包使用方式和操作时间仍会影响隐私效果。

### 存款

1. 连接兼容 Solana 的钱包，并使用 Solana Mainnet。
2. 选择 `SOL` 和固定面额的池子，例如 `1 SOL` 或 `10 SOL`。

   <figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

3. 点击存款，并安全保存浏览器生成的私密 note。

   <figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
提款必须使用私密 note。Voidify 无法找回遗失的 note；任何取得 note 的人都可以领取该笔存款。
{% endhint %}

4. 在钱包中确认交易。
5. 提款前等待同一池子出现更多存款，以提高匿名集。

### 提款

1. 打开 **Withdraw** 页面。
2. 粘贴私密 note，并填写收款地址。

   <figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

3. 使用系统自动选择的 relayer，或手动选择活跃 relayer。

   <figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

4. 点击 **Withdraw** 并确认。

   <figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### 保护你的 Note

* 不要分享、截图或将 note 上传至云盘或聊天工具。
* 如重视隐私，请勿重复使用存款钱包和收款钱包。
* 成功提款后，可根据合规需求保存或删除已使用的 note。

***

## Русский

Voidify позволяет вносить активы фиксированного номинала в пулы приватности и позднее выводить их с помощью доказательств нулевого разглашения. Способ хранения note, использование кошельков и время действий по-прежнему влияют на приватность.

### Депозит

1. Подключите совместимый с Solana кошелек и используйте Solana Mainnet.
2. Выберите `SOL` и пул фиксированного номинала, например `1 SOL` или `10 SOL`.

   <figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

3. Нажмите кнопку депозита и надежно сохраните приватную note, созданную в браузере.

   <figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
Приватная note необходима для вывода. Voidify не может восстановить потерянную note, а любой, кто получит ее, сможет забрать депозит.
{% endhint %}

4. Подтвердите транзакцию в кошельке.
5. Перед выводом подождите дополнительных депозитов в том же пуле, чтобы увеличить набор анонимности.

### Вывод

1. Откройте вкладку **Withdraw**.
2. Вставьте приватную note и укажите адрес получателя.

   <figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

3. Используйте автоматически выбранный relayer или выберите активный relayer вручную.

   <figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

4. Нажмите **Withdraw** и подтвердите действие.

   <figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### Защитите свою Note

* Не передавайте note, не делайте снимки экрана и не загружайте ее в облачные или чат-сервисы.
* Если приватность важна, не используйте повторно кошельки депозита и получения.
* После успешного вывода сохраните или удалите использованную note в соответствии с вашими требованиями к подтверждению происхождения средств.

***

## 日本語

Voidify では、固定額の資産をプライバシープールへ預け入れ、後からゼロ知識証明で出金できます。Note の扱い、ウォレットの使用方法、操作のタイミングは引き続きプライバシーに影響します。

### 預入

1. Solana 対応ウォレットを接続し、Solana Mainnet を使用します。
2. `SOL` と、`1 SOL` または `10 SOL` などの固定額プールを選びます。

   <figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

3. 預入をクリックし、ブラウザで生成された秘密の note を安全に保存します。

   <figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

{% hint style="danger" %}
秘密の note は出金に必要です。Voidify は紛失した note を復元できず、note を取得した人は誰でもその預入を引き出せます。
{% endhint %}

4. ウォレットでトランザクションを確認します。
5. 匿名集合を大きくするため、出金前に同じプールへの追加預入を待ちます。

### 出金

1. **Withdraw** タブを開きます。
2. 秘密の note を貼り付け、受取アドレスを入力します。

   <figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

3. 自動選択された relayer を使用するか、有効な relayer を手動で選択します。

   <figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

4. **Withdraw** をクリックして確認します。

   <figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

### Note の保護

* Note を共有、スクリーンショット撮影、クラウドやチャットサービスへのアップロードをしないでください。
* プライバシーが重要な場合、預入用と受取用のウォレットを再利用しないでください。
* 出金成功後、コンプライアンス上の必要性に応じて使用済み note を保管または削除してください。
