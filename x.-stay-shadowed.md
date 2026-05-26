---
description: Tips to Remain Anonymous
---

# X. Stay Shadowed

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

## X. Stay Shadowed

Voidify breaks on-chain links between deposit and withdrawal addresses using zero-knowledge proofs. But true privacy depends not just on protocol design — it also depends on **you**.

Even with perfect on-chain cryptography, your browser, wallet, and behavior can leak identifying data.

This guide helps you avoid common pitfalls and protect your privacy.

***

#### 🧠 Privacy Is a Practice

Voidify handles privacy on-chain. You must protect it off-chain.

Leaked metadata — like IP addresses, RPC usage, browser fingerprints, wallet reuse, and note handling — can void the unlinkability Voidify gives you.

***

#### 🌐 Use Privacy-Aware Browsers (That Support Solana Wallets)

To use Voidify, you’ll need a browser that supports **Phantom**, **Solflare**, or similar Solana-compatible wallets — without sacrificing your privacy.

**✅ Recommended:**

* **Firefox (Desktop)** — solid privacy controls and works with Phantom.
* **Brave (Desktop)** — Chromium-based with better privacy defaults than Chrome.
* **Safari or Arc (macOS)** — works with Phantom; less privacy-customizable but cleaner than Chrome.

> ❌ Avoid **Google Chrome** — it tracks background activity and leaks session data by default.

***

**📌 Browser Tips:**

* Use **Private/Incognito Mode** for every Voidify session.
* Use a **dedicated browser profile** just for Voidify interactions.
* Clear **cookies, cache, and local storage** after each use.
* Don’t install unnecessary browser extensions — especially ad blockers, password managers, or analytics tools that run in the background.

***

#### 🛡️ Use a VPN (or Tor) — Hide Your IP

Your IP address can be used to correlate transactions, especially by relayers or RPC providers.

* Use a **reputable paid VPN** — avoid free providers that log or sell your data.
* Choose VPNs with **WireGuard** or **OpenVPN** support.
* For stronger anonymity, use **Tor Browser** to access Voidify (when supported).
* Avoid using your regular internet connection during sensitive operations.

***

#### 🔒 Handle Notes With Extreme Care

Your Voidify **note** is both your private withdrawal key and your cryptographic link to the deposit.

* If someone gets your note, they can steal your funds — or deanonymize your transaction.
* Don’t store notes in cloud storage, plain text, or browser memory.
* Use **encrypted password managers** or cold storage.
* Always delete the note after a successful withdrawal.

***

#### 👛 Use Clean Wallets

Using the same wallet for multiple actions (or multiple Voidify interactions) creates traceable links.

* Use **a new wallet for each deposit and each withdrawal.**
* Avoid withdrawing multiple deposits to the same address.
* Use **open-source wallets** like:
  * **Phantom** (with caution)
  * **Solflare**
  * **MetaMask**

> Avoid MetaMask (even with Solana support) unless self-hosted — it uses RPC endpoints like Infura, which log usage and IPs.

***

#### ⌛ Wait to Withdraw — Don’t Rush

If you deposit and withdraw immediately, it's easier to link your actions.

* Wait until other users have deposited after you.
* Monitor the **anonymity set** (coming in Voidify v1 stats dashboard).
* The more activity between your deposit and withdrawal, the better your privacy.

***

#### 🧩 Fragment Large Balances

Big deposits into low-activity pools stand out.

* Break large amounts into **multiple smaller deposits**.
* Use pools with **high volume and frequent activity**.
* Yes, fees may be slightly higher — but your privacy will be significantly stronger.

***

#### 🔁 Rotate Relayers

Relayers help protect your identity by submitting withdrawal transactions on your behalf.

But if you use the **same relayer for every withdrawal**, patterns can form.

* Rotate relayers each time you withdraw.
* Don’t withdraw multiple notes through the same relayer.
* In future versions, you’ll be able to discover new relayers automatically.

***

#### 🧹 Clean Up After Yourself

Data stored in your browser or extension can betray your privacy — even across wallets.

* After each session:
  * Clear **cookies**
  * Clear **localStorage**
  * Clear **cache**
  * Clear **browsing history**
* Use **Incognito Mode** or dedicated, isolated profiles.

***

#### ⛽ Vary Fee Settings

Bots and analytics tools can fingerprint behavior like:

* Gas/compute unit values
* Transaction size
* Slippage parameters

Try not to use default settings every time.

* Add small randomization to gas or compute unit values if possible.
* Don’t copy-paste fee settings between deposit and withdrawal.

***

#### ✅ Final Summary

Voidify gives you cryptographic privacy on-chain — but the rest is up to you.

**Do this every time:**

* Use clean, privacy-respecting browsers
* Use a VPN or Tor
* Isolate your wallets
* Store notes securely
* Rotate relayers
* Clear all browser data
* Don’t rush your withdrawals

> **Privacy is earned through discipline.** Voidify gives you the tools — you supply the practice.

***

## 中文Voidify 会打破存款地址与提款地址之间的链上联系，但链下元数据和用户行为模式仍可能泄露信息。

### 操作隐私清单

* 使用专门用于 Voidify 的注重隐私的浏览器配置，并配合兼容的 Solana 钱包。
* 与应用交互时，可考虑使用可信的 VPN 或其他网络隐私保护手段。
* 在可行情况下使用新钱包，并避免将多笔无关提款发送到同一收款地址。
* 绝不要暴露私密 note。任何拥有 note 的人都可以领取存款。
* 安全保存 note，不要存入未加密文件、截图、聊天记录或云存储。
* 不要在存款后立即提款。等待同一池子出现更多活动可增加可能来源。
* 优先使用独立活动更多的池子，避免在低活动池中让存款格外显眼。
* 提款时使用 relayer，并避免重复明显的行为模式。
* 完成操作后清理本地浏览数据并删除敏感痕迹。

{% hint style="warning" %}
密码学保护的是链上联系；它无法保护由设备、网络、钱包复用、操作时间或 note 处理方式所泄露的元数据。
{% endhint %}

***

## Русский

Voidify разрывает ончейн-связи между адресами депозита и вывода, но внецепочечные метаданные и поведение пользователя все еще могут раскрывать закономерности.

### Контрольный список приватности

* Используйте отдельный браузерный профиль с настройками приватности для Voidify и совместимый кошелек Solana.
* При работе с приложением рассмотрите надежный VPN или другую сетевую защиту приватности.
* По возможности используйте новые кошельки и не отправляйте несколько несвязанных выводов на один адрес получателя.
* Никогда не раскрывайте приватную note. Любой владелец note может забрать депозит.
* Храните notes безопасно и не помещайте их в незашифрованные файлы, снимки экрана, чаты или облачное хранилище.
* Не выводите средства сразу после внесения. Ожидание дополнительной активности в том же пуле увеличивает число возможных источников.
* Предпочитайте пулы с большей независимой активностью, а не редкие пулы, где депозит выделяется.
* Используйте relayers для вывода и избегайте повторяющихся узнаваемых шаблонов поведения.
* После завершения сеанса очищайте локальные данные браузера и удаляйте чувствительные артефакты.

{% hint style="warning" %}
Криптография защищает ончейн-связь. Она не может защитить метаданные, раскрытые через устройство, сеть, повторное использование кошелька, время операций или обращение с note.
{% endhint %}

***

## 日本語

Voidify は預入アドレスと出金アドレスのオンチェーン上の結び付きを断ちますが、オフチェーンのメタデータやユーザー行動からパターンが明らかになる可能性は残ります。

### 運用上のプライバシーチェックリスト

* Voidify 専用のプライバシーを意識したブラウザプロファイルと、対応する Solana ウォレットを使用します。
* アプリケーションを利用する際は、信頼できる VPN などのネットワークプライバシー保護を検討してください。
* 可能な限り新しいウォレットを使い、無関係な複数の出金を同じ受取アドレスへ送らないでください。
* 秘密の note を決して公開しないでください。Note を持つ人は預入を引き出せます。
* Note は安全に保管し、暗号化されていないファイル、スクリーンショット、チャット、クラウドストレージに置かないでください。
* 預入直後に出金しないでください。同じプールでの活動を待つことで、もっともらしい出所の候補が増えます。
* 活動の少ないプールより、独立した活動の多いプールを優先してください。
* 出金には relayer を使用し、認識しやすい行動パターンの繰り返しを避けてください。
* セッション終了後はローカルのブラウザデータを消去し、機密性のある痕跡を削除してください。

{% hint style="warning" %}
暗号技術が保護するのはオンチェーン上の関連です。デバイス、ネットワーク、ウォレット再利用、タイミング、note の扱いを通じて公開されたメタデータまでは保護できません。
{% endhint %}
