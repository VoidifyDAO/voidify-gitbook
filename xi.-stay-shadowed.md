---
description: Tips to Remain Anonymous
---

# XI. Stay Shadowed

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

### XI. Stay Shadowed

Voidify breaks on-chain links between deposit and withdrawal addresses using zero-knowledge proofs. But true privacy depends not just on protocol design — it also depends on **you**.

Even with perfect on-chain cryptography, your browser, wallet, and behavior can leak identifying data.

This guide helps you avoid common pitfalls and protect your privacy.

***

##### 🧠 Privacy Is a Practice

Voidify handles privacy on-chain. You must protect it off-chain.

Leaked metadata — like IP addresses, RPC usage, browser fingerprints, wallet reuse, and note handling — can void the unlinkability Voidify gives you.

***

##### 🌐 Use Privacy-Aware Browsers (That Support Solana Wallets)

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

##### 🛡️ Use a VPN (or Tor) — Hide Your IP

Your IP address can be used to correlate transactions, especially by relayers or RPC providers.

* Use a **reputable paid VPN** — avoid free providers that log or sell your data.
* Choose VPNs with **WireGuard** or **OpenVPN** support.
* For stronger anonymity, use **Tor Browser** to access Voidify (when supported).
* Avoid using your regular internet connection during sensitive operations.

***

##### 🔒 Handle Notes With Extreme Care

Your Voidify **note** is both your private withdrawal key and your cryptographic link to the deposit.

* If someone gets your note, they can steal your funds — or deanonymize your transaction.
* Don’t store notes in cloud storage, plain text, or browser memory.
* Use **encrypted password managers** or cold storage.
* Always delete the note after a successful withdrawal.

***

##### 👛 Use Clean Wallets

Using the same wallet for multiple actions (or multiple Voidify interactions) creates traceable links.

* Use **a new wallet for each deposit and each withdrawal.**
* Avoid withdrawing multiple deposits to the same address.
* Use **open-source wallets** like:
  * **Phantom** (with caution)
  * **Solflare**
  * **MetaMask**

> Avoid MetaMask (even with Solana support) unless self-hosted — it uses RPC endpoints like Infura, which log usage and IPs.

***

##### ⌛ Choose Timing for the Pool You Use

Timing affects Classic and Nova differently.

* **Classic:** wait for more deposits in the same denomination. A rare denomination only gains peers when that exact pool receives activity.
* **Nova:** there is no need to wait for another deposit of the exact same amount. Different amounts share the token's Nova pool, so large deposits do not have to wait for another identical large deposit.
* In either mode, an immediate withdrawal with a distinctive public amount or timing pattern may still be correlated. More unrelated pool activity generally improves practical privacy.

***

##### 🧩 Handle Large Balances Deliberately

Big deposits into low-activity pools stand out.

* In **Classic**, choose active denominations and split an amount only when doing so improves the available anonymity sets.
* In **Nova**, you can deposit a large amount without waiting for the same large denomination to appear, then withdraw only what you need while keeping the remainder private.
* Splitting a distinctive amount into a predictable sequence can create its own fingerprint. Prefer natural-looking timing and active pools over mechanical fragmentation.

***

##### 🔁 Rotate Relayers

Relayers help protect your identity by submitting withdrawal transactions on your behalf.

But if you use the **same relayer for every withdrawal**, patterns can form.

* Rotate relayers each time you withdraw.
* Don’t withdraw multiple notes through the same relayer.
* In future versions, you’ll be able to discover new relayers automatically.

***

##### 🧹 Clean Up After Yourself

Data stored in your browser or extension can betray your privacy — even across wallets.

* After each session:
  * Clear **cookies**
  * Clear **localStorage**
  * Clear **cache**
  * Clear **browsing history**
* Use **Incognito Mode** or dedicated, isolated profiles.

***

##### ⛽ Vary Fee Settings

Bots and analytics tools can fingerprint behavior like:

* Gas/compute unit values
* Transaction size
* Slippage parameters

Try not to use default settings every time.

* Add small randomization to gas or compute unit values if possible.
* Don’t copy-paste fee settings between deposit and withdrawal.

***

##### ✅ Final Summary

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

## 中文

### XI. 保持隐身

Voidify 使用零知识证明打破存款地址与提款地址之间的链上联系。但真正的隐私不只取决于协议设计，也取决于**你自己**。

即使链上密码学是完美的，你的浏览器、钱包和行为也可能泄露可识别数据。

本指南帮助你避开常见陷阱并保护隐私。

***

##### 🧠 隐私是一种实践

Voidify 处理链上隐私。你必须保护链下隐私。

泄露的元数据（例如 IP 地址、RPC 使用、浏览器指纹、钱包复用和 note 处理方式）可能让 Voidify 提供的不可链接性失效。

***

##### 🌐 使用注重隐私的浏览器（并支持 Solana 钱包）

要使用 Voidify，你需要一个支持 **Phantom**、**Solflare** 或类似 Solana 兼容钱包的浏览器，同时不能牺牲隐私。

**✅ 推荐：**

* **Firefox（桌面端）** — 具备可靠的隐私控制，并可与 Phantom 配合使用。
* **Brave（桌面端）** — 基于 Chromium，但默认隐私设置优于 Chrome。
* **Safari 或 Arc（macOS）** — 可与 Phantom 配合使用；隐私可定制性较弱，但比 Chrome 更干净。

> ❌ 避免使用 **Google Chrome** — 默认情况下它会追踪后台活动并泄露会话数据。

***

**📌 浏览器建议：**

* 每次 Voidify 会话都使用**隐私/无痕模式**。
* 为 Voidify 交互使用**专用浏览器配置文件**。
* 每次使用后清除 **cookies、cache 和 local storage**。
* 不要安装不必要的浏览器扩展，尤其是会在后台运行的广告拦截器、密码管理器或分析工具。

***

##### 🛡️ 使用 VPN（或 Tor）隐藏你的 IP

你的 IP 地址可能被用于关联交易，尤其是被 relayers 或 RPC providers 关联。

* 使用**信誉良好的付费 VPN**，避免会记录或出售数据的免费服务商。
* 选择支持 **WireGuard** 或 **OpenVPN** 的 VPN。
* 如需更强匿名性，在支持时使用 **Tor Browser** 访问 Voidify。
* 在敏感操作期间避免使用日常网络连接。

***

##### 🔒 极其谨慎地处理 Notes

你的 Voidify **note** 既是你的私密提款密钥，也是你与存款之间的密码学链接。

* 如果有人获得你的 note，他们可以窃取你的资金，或者去匿名化你的交易。
* 不要把 notes 存入云存储、明文文件或浏览器内存。
* 使用**加密密码管理器**或冷存储。
* 成功提款后始终删除 note。

***

##### 👛 使用干净钱包

使用同一个钱包进行多个操作（或多次 Voidify 交互）会创造可追踪链接。

* 为每次存款和每次提款使用**新钱包**。
* 避免将多笔存款提款到同一个地址。
* 使用**开源钱包**，例如：
  * **Phantom**（需谨慎）
  * **Solflare**
  * **MetaMask**

> 除非自托管，否则避免使用 MetaMask（即使支持 Solana）——它使用 Infura 等 RPC endpoints，这些服务会记录使用情况和 IP。

***

##### ⌛ 根据所用隐私池选择时间

时间对 Classic 和 Nova 的影响不同。

* **Classic：**等待同一面额池出现更多存款。冷门面额只有在对应池产生新活动时，才会增加同类候选项。
* **Nova：**不需要等待另一笔完全相同金额的存款。不同金额共享同一代币的 Nova 池，因此大额存款不必等待另一笔相同大额出现。
* 无论使用哪种模式，如果立即提取一个独特的公开金额，或形成明显的时间模式，仍可能被关联。更多无关的池内活动通常会提升实际隐私。

***

##### 🧩 谨慎处理大额余额

向低活跃池进行大额存款会非常显眼。

* 使用 **Classic** 时，应选择活跃面额；只有在拆分确实能进入更活跃匿名集时，才考虑拆分金额。
* 使用 **Nova** 时，可以直接存入大额资金，不必等待相同大额出现；之后只提取所需部分，并让剩余余额继续保持私密。
* 把独特金额机械地拆成一串可预测的小额，也可能形成新的指纹。相比固定拆分模式，应优先考虑自然的操作时间和活跃池。

***

##### 🔁 轮换 Relayers

Relayers 通过代表你提交提款交易来帮助保护你的身份。

但如果每次提款都使用**同一个 relayer**，模式可能形成。

* 每次提款都轮换 relayer。
* 不要通过同一个 relayer 提取多份 notes。
* 在未来版本中，你将能够自动发现新的 relayers。

***

##### 🧹 清理操作痕迹

存储在浏览器或扩展中的数据可能暴露你的隐私，即使你切换了钱包。

* 每次会话后：
  * 清除 **cookies**
  * 清除 **localStorage**
  * 清除 **cache**
  * 清除**浏览历史**
* 使用**无痕模式**或专用、隔离的配置文件。

***

##### ⛽ 改变费用设置

Bots 和分析工具可以根据以下行为建立指纹：

* Gas/compute unit values
* Transaction size
* Slippage parameters

尽量不要每次都使用默认设置。

* 如果可能，对 gas 或 compute unit values 加入小幅随机化。
* 不要在存款和提款之间复制粘贴相同费用设置。

***

##### ✅ 最终总结

Voidify 为你提供链上密码学隐私，但其余部分取决于你。

**每次都这样做：**

* 使用干净、尊重隐私的浏览器
* 使用 VPN 或 Tor
* 隔离你的钱包
* 安全保存 notes
* 轮换 relayers
* 清除所有浏览器数据
* 不要急于提款

> **隐私来自纪律。** Voidify 提供工具，而实践由你完成。

***

## Русский

### XI. Оставайтесь в тени

Voidify разрывает ончейн-связи между адресами депозита и вывода с помощью доказательств нулевого разглашения. Но настоящая приватность зависит не только от дизайна протокола — она также зависит от **вас**.

Даже при идеальной ончейн-криптографии ваш браузер, кошелек и поведение могут раскрывать идентифицирующие данные.

Это руководство поможет избежать распространенных ошибок и защитить приватность.

***

##### 🧠 Приватность — это практика

Voidify обеспечивает приватность ончейн. Вы должны защищать ее офчейн.

Утекшие метаданные — IP-адреса, использование RPC, браузерные отпечатки, повторное использование кошельков и обращение с note — могут обнулить несвязываемость, которую дает Voidify.

***

##### 🌐 Используйте браузеры с учетом приватности (и поддержкой Solana-кошельков)

Для использования Voidify нужен браузер, который поддерживает **Phantom**, **Solflare** или похожие Solana-совместимые кошельки, не жертвуя вашей приватностью.

**✅ Рекомендуется:**

* **Firefox (Desktop)** — надежные настройки приватности и совместимость с Phantom.
* **Brave (Desktop)** — основан на Chromium, но имеет более приватные настройки по умолчанию, чем Chrome.
* **Safari или Arc (macOS)** — работает с Phantom; менее гибок по приватности, но чище Chrome.

> ❌ Избегайте **Google Chrome** — он по умолчанию отслеживает фоновую активность и раскрывает данные сессии.

***

**📌 Советы по браузеру:**

* Используйте **Private/Incognito Mode** для каждой сессии Voidify.
* Используйте **отдельный профиль браузера** только для взаимодействий с Voidify.
* После каждого использования очищайте **cookies, cache и local storage**.
* Не устанавливайте лишние расширения браузера, особенно блокировщики рекламы, менеджеры паролей или аналитические инструменты, работающие в фоне.

***

##### 🛡️ Используйте VPN (или Tor), чтобы скрыть IP

Ваш IP-адрес может использоваться для корреляции транзакций, особенно relayers или RPC providers.

* Используйте **надежный платный VPN** и избегайте бесплатных провайдеров, которые логируют или продают данные.
* Выбирайте VPN с поддержкой **WireGuard** или **OpenVPN**.
* Для более сильной анонимности используйте **Tor Browser** для доступа к Voidify, когда это поддерживается.
* Избегайте использования обычного интернет-соединения во время чувствительных операций.

***

##### 🔒 Обращайтесь с Notes крайне осторожно

Ваша Voidify **note** — это одновременно приватный ключ вывода и криптографическая связь с депозитом.

* Если кто-то получит вашу note, он сможет украсть средства или деанонимизировать транзакцию.
* Не храните notes в облаке, открытом тексте или памяти браузера.
* Используйте **зашифрованные менеджеры паролей** или холодное хранение.
* Всегда удаляйте note после успешного вывода.

***

##### 👛 Используйте чистые кошельки

Использование одного и того же кошелька для нескольких действий или нескольких взаимодействий с Voidify создает отслеживаемые связи.

* Используйте **новый кошелек для каждого депозита и каждого вывода**.
* Избегайте вывода нескольких депозитов на один и тот же адрес.
* Используйте **open-source wallets**, например:
  * **Phantom** (с осторожностью)
  * **Solflare**
  * **MetaMask**

> Избегайте MetaMask (даже с поддержкой Solana), если он не self-hosted: он использует RPC endpoints вроде Infura, которые логируют использование и IP.

***

##### ⌛ Выбирайте timing с учетом типа pool

Timing влияет на Classic и Nova по-разному.

* **Classic:** ждите активности в том же номинале. Редкий номинал получает новые варианты только при депозитах в этот exact pool.
* **Nova:** не нужно ждать депозит точно такого же размера. Разные суммы используют Nova pool выбранного token, поэтому крупный депозит не обязан ждать другой идентичный крупный депозит.
* В обоих режимах немедленный вывод с уникальной публичной суммой или характерным timing может быть сопоставлен. Дополнительная независимая активность обычно улучшает практическую privacy.

***

##### 🧩 Обдуманно работайте с крупными балансами

Крупные депозиты в пулы с низкой активностью выделяются.

* В **Classic** выбирайте активные номиналы и делите сумму только тогда, когда это действительно дает более сильные anonymity sets.
* В **Nova** можно внести крупную сумму без ожидания такого же крупного депозита, затем вывести только нужную часть и оставить остаток приватным.
* Предсказуемое дробление уникальной суммы само может стать fingerprint. Естественный timing и активный pool полезнее механической схемы.

***

##### 🔁 Меняйте Relayers

Relayers помогают защищать личность, отправляя транзакции вывода от вашего имени.

Но если вы используете **одного и того же relayer для каждого вывода**, могут формироваться паттерны.

* Меняйте relayer при каждом выводе.
* Не выводите несколько notes через одного и того же relayer.
* В будущих версиях вы сможете автоматически находить новых relayers.

***

##### 🧹 Убирайте следы после себя

Данные, сохраненные в браузере или расширении, могут выдать вашу приватность даже между разными кошельками.

* После каждой сессии:
  * очистите **cookies**;
  * очистите **localStorage**;
  * очистите **cache**;
  * очистите **browsing history**.
* Используйте **Incognito Mode** или выделенные изолированные профили.

***

##### ⛽ Меняйте настройки комиссий

Боты и аналитические инструменты могут отпечатывать поведение по таким признакам, как:

* Gas/compute unit values
* Transaction size
* Slippage parameters

Старайтесь не использовать настройки по умолчанию каждый раз.

* По возможности добавляйте небольшую случайность в gas или compute unit values.
* Не копируйте настройки комиссий между депозитом и выводом.

***

##### ✅ Итоговое резюме

Voidify дает криптографическую приватность ончейн, но остальное зависит от вас.

**Делайте это каждый раз:**

* Используйте чистые браузеры, уважающие приватность
* Используйте VPN или Tor
* Изолируйте кошельки
* Надежно храните notes
* Меняйте relayers
* Очищайте все данные браузера
* Не спешите с выводом

> **Приватность достигается дисциплиной.** Voidify дает инструменты — практику обеспечиваете вы.

***

## 日本語

### XI. 影に留まる

Voidify はゼロ知識証明を使って、預入アドレスと出金アドレスのオンチェーンリンクを断ちます。しかし本当のプライバシーは、プロトコル設計だけでなく、**あなた自身**にも依存します。

オンチェーン暗号が完璧であっても、ブラウザ、ウォレット、行動によって識別情報が漏れる可能性があります。

このガイドは、よくある落とし穴を避け、プライバシーを守るためのものです。

***

##### 🧠 プライバシーは実践である

Voidify はオンチェーンのプライバシーを扱います。あなたはオフチェーンでそれを守らなければなりません。

IP アドレス、RPC 使用状況、ブラウザ指紋、ウォレット再利用、note の扱いなどのメタデータが漏れると、Voidify が提供する不可リンク性は無効化される可能性があります。

***

##### 🌐 プライバシーを意識したブラウザを使う（Solana ウォレット対応）

Voidify を使うには、**Phantom**、**Solflare**、または類似の Solana 対応ウォレットをサポートしつつ、プライバシーを犠牲にしないブラウザが必要です。

**✅ 推奨：**

* **Firefox（Desktop）** — しっかりしたプライバシー制御があり、Phantom と連携できます。
* **Brave（Desktop）** — Chromium ベースですが、Chrome よりも優れたプライバシーデフォルトを持ちます。
* **Safari または Arc（macOS）** — Phantom と連携できます。プライバシーのカスタマイズ性は低いものの、Chrome よりクリーンです。

> ❌ **Google Chrome** は避けてください。デフォルトでバックグラウンド活動を追跡し、セッションデータを漏らします。

***

**📌 ブラウザのヒント：**

* Voidify の各セッションで **Private/Incognito Mode** を使用します。
* Voidify とのやり取り専用の**ブラウザプロファイル**を使用します。
* 使用後は毎回 **cookies、cache、local storage** を消去します。
* 不要なブラウザ拡張機能をインストールしないでください。特に、バックグラウンドで動作する広告ブロッカー、パスワードマネージャー、分析ツールには注意してください。

***

##### 🛡️ VPN（または Tor）を使って IP を隠す

あなたの IP アドレスは、特に relayers や RPC providers によってトランザクションの相関に使われる可能性があります。

* **信頼できる有料 VPN** を使用し、データを記録または販売する無料プロバイダーは避けてください。
* **WireGuard** または **OpenVPN** をサポートする VPN を選択してください。
* より強い匿名性が必要な場合、対応していれば **Tor Browser** で Voidify にアクセスします。
* 機密性の高い操作中は、普段のインターネット接続を避けてください。

***

##### 🔒 Notes は極めて慎重に扱う

Voidify の **note** は、あなたの秘密の出金キーであり、預入への暗号学的リンクでもあります。

* 誰かが note を入手すると、資金を盗むか、トランザクションを匿名解除できます。
* Notes をクラウドストレージ、平文、ブラウザメモリに保存しないでください。
* **暗号化されたパスワードマネージャー**またはコールドストレージを使用してください。
* 出金に成功した後は、必ず note を削除してください。

***

##### 👛 クリーンなウォレットを使う

同じウォレットを複数の操作、または複数の Voidify interaction に使うと、追跡可能なリンクが作られます。

* **各預入と各出金ごとに新しいウォレット**を使用します。
* 複数の預入を同じアドレスへ出金することは避けてください。
* 次のような **open-source wallets** を使用します。
  * **Phantom**（慎重に）
  * **Solflare**
  * **MetaMask**

> Self-hosted でない限り、MetaMask（Solana 対応であっても）は避けてください。Infura のような RPC endpoints を使用し、使用状況や IP を記録します。

***

##### ⌛ Pool に応じて Timing を選ぶ

Timing の影響は Classic と Nova で異なります。

* **Classic：**同じ額面 pool に追加 deposit が入るのを待ちます。希少な額面は、その exact pool に activity がなければ候補が増えません。
* **Nova：**完全に同じ金額の deposit を待つ必要はありません。異なる金額が同じ token の Nova pool を使うため、大口 deposit も同額の別 deposit を待つ必要がありません。
* どちらでも、特徴的な公開金額を即時 withdraw したり明確な timing pattern を作ったりすると、相関される可能性があります。無関係な pool activity が増えるほど実用上の privacy は通常向上します。

***

##### 🧩 大きな残高を慎重に扱う

活動の少ないプールへの大口預入は目立ちます。

* **Classic** では active な額面を選び、分割によってより強い anonymity sets を利用できる場合だけ分割を検討します。
* **Nova** では、同額の大口 deposit を待たずに大きな金額を deposit し、必要な分だけ withdraw して残りを private に保てます。
* 特徴的な金額を規則的に分割すると、それ自体が fingerprint になります。機械的な分割より、自然な timing と active pool を優先してください。

***

##### 🔁 Relayers をローテーションする

Relayers は、あなたの代わりに出金トランザクションを送信することで身元を保護します。

ただし、**毎回同じ relayer** を使うと、パターンが形成される可能性があります。

* 出金のたびに relayer をローテーションします。
* 複数の notes を同じ relayer 経由で出金しないでください。
* 将来のバージョンでは、新しい relayers を自動的に発見できるようになります。

***

##### 🧹 自分の痕跡を片付ける

ブラウザや拡張機能に保存されたデータは、ウォレットをまたいでもプライバシーを裏切る可能性があります。

* 各セッション後に：
  * **cookies** を消去
  * **localStorage** を消去
  * **cache** を消去
  * **browsing history** を消去
* **Incognito Mode** または専用の隔離プロファイルを使用します。

***

##### ⛽ 手数料設定を変える

Bots や分析ツールは、次のような行動から指紋を取ることができます。

* Gas/compute unit values
* Transaction size
* Slippage parameters

毎回デフォルト設定を使わないようにしてください。

* 可能であれば、gas または compute unit values に小さなランダム性を加えます。
* 預入と出金の間で fee settings をコピー＆ペーストしないでください。

***

##### ✅ 最終まとめ

Voidify はオンチェーンの暗号学的プライバシーを提供します。しかし残りはあなた次第です。

**毎回これを行ってください：**

* クリーンでプライバシーを尊重するブラウザを使う
* VPN または Tor を使う
* ウォレットを隔離する
* Notes を安全に保管する
* Relayers をローテーションする
* すべてのブラウザデータを消去する
* 出金を急がない

> **プライバシーは規律によって得られます。** Voidify はツールを提供し、実践するのはあなたです。
