---
description: Voidify Protocol Fees
---

# III. Voidify Fee Structure & Token Utility

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2F29p8GK5zXCWfQawWGaEe%2Fvoidify%20fees.png?alt=media&#x26;token=d14cf7b1-72f5-4751-8761-469ee9a8bd6e" alt="" width="250"><figcaption></figcaption></figure>

***

## English

### Withdrawal Fees

Voidify supports two withdrawal paths:

**Relayer withdrawal**

* A registered relayer submits the transaction for the user.
* The relayer sets its fee, up to the protocol maximum of `10%`.
* A DAO refund fee is paid in SOL to the relayer; an equivalent value of VOID is deducted from that relayer's stake and routed under protocol rules.
* The recipient receives the deposit amount minus applicable fees.

**Direct withdrawal**

* The user submits the transaction without a relayer and pays the network fee.
* No relayer fee applies.
* The DAO fee is applied under the on-chain configuration.
* This path is available when the user does not use a relayer.

### VOID Token Utility

VOID is the relayer staking token. Holders can stake the required amount to register a relayer, process withdrawals, earn SOL fees, and manage their fee and service endpoint.

Fees and configuration are enforced by smart contract logic. Fee amounts are part of the verified withdrawal data, and token-to-SOL conversion uses the configured oracle.

***

## 中文

### 提款手续费

Voidify 支持两种提款方式：

**Relayer 提款**

* 已注册的 relayer 代表用户提交交易。
* Relayer 设置自身手续费，最高不超过协议上限 `10%`。
* DAO refund fee 以 SOL 支付给 relayer；相等价值的 VOID 会从其质押中扣除，并按协议规则分配。
* 收款人收到扣除适用手续费后的存款金额。

**直接提款**

* 用户不使用 relayer，自行提交交易并支付网络手续费。
* 不收取 relayer 手续费。
* DAO fee 按链上配置收取。
* 用户在不使用 relayer 时可选择此方式。

### VOID 代币用途

VOID 是 relayer 的质押代币。持有人可质押所需数量注册 relayer、处理提款、赚取 SOL 手续费，并管理手续费率和服务地址。

手续费和配置均由智能合约逻辑执行。手续费金额属于经验证的提款数据，VOID 与 SOL 的换算使用已配置的预言机。

***

## Русский

### Комиссии за вывод

Voidify поддерживает два способа вывода:

**Вывод через relayer**

* Зарегистрированный relayer отправляет транзакцию от имени пользователя.
* Relayer устанавливает свою комиссию в пределах максимума протокола `10%`.
* DAO refund fee выплачивается relayer в SOL; эквивалентная стоимость в VOID списывается из его стейка и распределяется по правилам протокола.
* Получатель получает сумму депозита за вычетом применимых комиссий.

**Прямой вывод**

* Пользователь отправляет транзакцию без relayer и оплачивает сетевую комиссию.
* Комиссия relayer отсутствует.
* DAO fee применяется согласно ончейн-настройкам.
* Этот путь доступен, если пользователь не использует relayer.

### Назначение токена VOID

VOID является токеном стейкинга relayer. Владельцы могут застейкать требуемую сумму, зарегистрировать relayer, обрабатывать выводы, получать комиссии в SOL и управлять ставкой комиссии и адресом сервиса.

Комиссии и конфигурация исполняются логикой смарт-контракта. Размеры комиссий входят в проверяемые данные вывода, а преобразование VOID в SOL использует настроенный оракул.

***

## 日本語

### 出金手数料

Voidify は二つの出金経路をサポートします。

**Relayer 経由の出金**

* 登録済みの relayer がユーザーに代わってトランザクションを送信します。
* Relayer は、プロトコル上限 `10%` 以内で自身の手数料を設定します。
* DAO refund fee は SOL で relayer に支払われ、同等価値の VOID がそのステークから差し引かれ、プロトコル規則に従って配分されます。
* 受取人は適用される手数料を差し引いた預入額を受け取ります。

**直接出金**

* ユーザーが relayer を使わずにトランザクションを送信し、ネットワーク手数料を負担します。
* Relayer 手数料は発生しません。
* DAO fee はオンチェーン設定に従って適用されます。
* Relayer を使用しない場合に利用できます。

### VOID トークンの用途

VOID は relayer のステーキングトークンです。保有者は必要額をステークして relayer を登録し、出金を処理して SOL 手数料を受け取り、手数料率やサービス URL を管理できます。

手数料と設定はスマートコントラクトのロジックによって実行されます。手数料額は検証対象の出金データに含まれ、VOID と SOL の換算には設定されたオラクルが使用されます。
