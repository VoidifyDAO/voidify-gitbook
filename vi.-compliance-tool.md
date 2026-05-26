# VI. Compliance tool

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

## Compliance Tool

By design, all blockchain transactions are publicly visible, which can deprive users of their right to financial privacy. Anyone can inspect a wallet's transaction history, trace asset flows, and build a detailed picture of a user's on-chain activity. In response to this structural problem, the Voidify protocol enables users to regain financial privacy by breaking the on-chain link between a source address and a destination address.

However, preserving privacy and financial freedom should never come at the cost of being unable to demonstrate lawful source of funds when necessary. The right to privacy includes the right to control what information is disclosed, and to whom it is disclosed.

To address this need, Voidify includes a **Compliance Tool** that enables users to prove the origin of their funds. Using the Voidify Note generated after each deposit, the tool can issue a **cryptographically verified proof of transactional history** based on the Solana addresses used to deposit and withdraw assets.

Therefore, if you ever need to prove the origin of assets withdrawn from a Voidify pool, you may use the Voidify Compliance Tool to generate a compliance report.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## How to Use the Compliance Tool

Each time a deposit is made through Voidify, the protocol generates a unique **Voidify Note**. This Note is required to later withdraw the deposited assets to a withdrawal address. The same Note can also be used, when necessary, to generate a **Compliance Report** proving the origin of the withdrawn assets.

To generate a Compliance Report, the user only needs to enter the Voidify Note into the dedicated input field of the Compliance Tool.

The report is generated solely from data controlled by the user and publicly verifiable on-chain information. It does not require any privileged access, administrative approval, or protocol-level backdoor.

***

## Before Withdrawal

If the Note has **not yet been spent** (that is, the assets have not yet been withdrawn), the Compliance Tool provides information related to the deposit only, including:

* the transaction signature of the deposit;
* the source address;
* the commitment hash.

The commitment is the hashed value generated for the deposit and submitted to the Voidify smart contract to represent the deposit within the protocol.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

At this stage, the Compliance Tool can prove that a given deposit was made from a particular source address, even before any withdrawal has occurred.

***

## After Withdrawal

If the Note **has been spent** (that is, the assets were withdrawn using that Note), the Compliance Tool expands the report by including:

* the transaction signature of the withdrawal;
* the destination address;
* the nullifier hash.

The nullifier hash is a public value submitted on-chain during withdrawal to prove that the Note has been spent only once and to prevent double-spending.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

At this stage, the tool allows the user to re-establish the link between the original source address and the withdrawal destination address, thereby proving the transaction history of the assets involved.

***

## Purpose of the Compliance Tool

The Voidify Compliance Tool is designed for lawful, user-directed disclosure in situations where a user may need to prove the source of assets held in a withdrawal address. This may include, for example:

* exchange source-of-funds reviews;
* accounting or audit procedures;
* counterparty due diligence;
* legal or regulatory inquiries directed at the user.

Importantly, the Compliance Tool does **not** weaken privacy for all users. It does not introduce any master tracing key, administrator override, or global surveillance capability. Only the user in possession of the relevant Note can generate the report for that specific deposit and withdrawal history.

In this way, Voidify preserves privacy by default while still enabling users to prove lawful source of funds when needed.

***

This information can also be downloaded under a PDF format, making it is easier to get sent to any desired third part:<br>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## Summary

The Compliance Tool allows users to selectively and voluntarily prove the origin of their funds without compromising the privacy guarantees of the protocol as a whole. It is not a surveillance feature, but a user protection feature: one that ensures privacy and compliance can coexist when disclosure is initiated by the user and limited to what is necessary.

***

## 中文### 用途

Voidify 会打破存款地址和提款地址之间公开可见的链上联系。合规工具让用户在确需披露时，主动证明自己所提款项的来源。

只有持有相关 Voidify note 的用户才能为该笔存款生成报告。该工具不存在全局追踪密钥、管理员绕过权限或全局监控能力。

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### 生成报告

将存款时生成的 Voidify note 输入合规工具。报告使用用户控制的 note 数据和链上可公开验证的记录。

提款前，报告可包含：

* 存款交易签名。
* 来源地址。
* Commitment hash。

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Note 已使用后，报告还可包含：

* 提款交易签名。
* 目标地址。
* Nullifier hash。

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

报告可下载为 PDF，用于资金来源审查、会计或审计、交易对手尽职调查，以及向用户提出的法律或监管请求。

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## Русский

### Назначение

Voidify разрывает публично видимую ончейн-связь между адресом депозита и адресом вывода. Compliance Tool предоставляет пользователю добровольный способ доказать происхождение собственных выведенных средств, когда раскрытие необходимо.

Только пользователь, владеющий соответствующей Voidify note, может создать отчет для данного депозита. Инструмент не предоставляет главного ключа трассировки, административного обхода или возможности глобального наблюдения.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### Создание отчета

Введите Voidify note, созданную при внесении средств, в Compliance Tool. Отчет использует данные note под контролем пользователя и публично проверяемые ончейн-записи.

До вывода отчет может включать:

* Подпись транзакции депозита.
* Адрес источника.
* Commitment hash.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

После расходования note отчет также может включать:

* Подпись транзакции вывода.
* Адрес назначения.
* Nullifier hash.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Отчет можно загрузить в формате PDF для проверки происхождения средств, бухгалтерии, аудита, проверки контрагента либо юридических и регуляторных запросов, адресованных пользователю.

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## 日本語

### 目的

Voidify は、預入アドレスと出金アドレスの間に公開されるオンチェーン上の関連を断ちます。Compliance Tool は、開示が必要な場合に、ユーザーが自身の出金資金の出所を自発的に証明できるようにします。

対象の Voidify note を保有するユーザーだけが、その預入に関するレポートを生成できます。このツールには、全体を追跡するマスターキー、管理者による回避機能、またはグローバルな監視能力はありません。

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

### レポートの生成

預入時に生成された Voidify note を Compliance Tool に入力します。レポートは、ユーザーが管理する note データと、公開検証可能なオンチェーン記録を利用します。

出金前のレポートには次の情報を含められます。

* 預入トランザクション署名。
* 送金元アドレス。
* Commitment hash。

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Note が使用された後のレポートには、さらに次の情報を含められます。

* 出金トランザクション署名。
* 送金先アドレス。
* Nullifier hash。

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

レポートは PDF としてダウンロードでき、資金源確認、会計・監査、取引相手のデューデリジェンス、またはユーザー宛ての法的・規制上の要請に利用できます。

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>
