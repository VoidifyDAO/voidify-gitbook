---
description: Voidify Protocol Fees
---

# III. Voidify Fee Structure & Token Utility

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

Voidify uses a transparent, permissionless fee structure designed to sustain the protocol, support contributor participation, and promote user privacy — all without introducing custodial risk or centralized fee collection.

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2F29p8GK5zXCWfQawWGaEe%2Fvoidify%20fees.png?alt=media&#x26;token=d14cf7b1-72f5-4751-8761-469ee9a8bd6e" alt="" width="250"><figcaption></figcaption></figure>

***

#### **Fee Breakdown**

#### Two Withdrawal Modes

\
Voidify supports two withdrawal paths, each with a distinct fee model:

**1. Relayer Withdraw (via registered relayer)**

Users submit withdrawal requests through a registered relayer, preserving privacy by not requiring the recipient to pay gas.

* **Relayer Fee**: Set by each relayer individually (default 0.1%)(max 10%. The fee level affects the random selection order of relayers). This SOL goes directly to the relayer.
* **DAO Refund Fee**: Set by the DAO authority (default 0.3%)(max 10%). The SOL equivalent goes to the relayer, while the token equivalent is deducted from the relayer's stake and sent to the DAO treasury (Once staking goes live, it will be changed to be sent to the stakers).
* **Recipient receives**: Deposit amount minus both fees

**2. Direct Withdraw (no relayer)(Use this only when all relayers are unavailable)**

Users withdraw directly without a relayer. The user pays gas themselves.

* **Relayer Fee**: Always 0 (no relayer involved)
* **DAO Fee**: Set by the DAO authority (default 5%)(max 10%). This SOL goes to the DAO treasury(Once staking goes live, it will be changed to be sent to the stakers).
* **Recipient receives**: Deposit amount minus DAO fee

***

### ∅ Token Utility

The ∅ token serves as the **relayer staking token** within the Voidify protocol. It is required to participate as a relayer and earn fees from processing withdrawals.

#### For Relayers (∅ Token Holders)

* ✅ **Register as a relayer** by staking ∅ tokens
* ✅ **Earn SOL** from every withdrawal processed
* ✅ **Set custom fee rates** (up to 10%)
* ✅ **Manage your relayer** (add stake, update fees, update service URL)
* ✅ **Contribute to decentralized privacy infrastructure**

See the dedicated **Relayer Documentation** for full details on registration, economics, and operations.

***

#### **Why This Model?**

This model is designed to:

* **Incentivize relayer growth** — relayers earn SOL from every withdrawal they process, creating a competitive marketplace
* **Sustain the protocol** — DAO fees fund ongoing development
* **Ensure relayer accountability** — staking mechanisms deter malicious behavior
* **Maintain decentralization** — anyone can become a relayer; fee rates are market-driven

***

### Fee Architecture

* All fees are calculated and enforced **autonomously via smart contract logic**
* Fee parameters are validated on-chain — the ZK proof commits to the exact fee amounts
* Token-to-SOL conversion uses **oracle** for real-time pricing
* There is **no custodial control** or manual fee routing
* All configuration changes require **DAO authority** signature

***

### Summary

The ∅ token is the **relayer staking token** within Voidify. It enables holders to register as relayers, earn SOL from processing withdrawals, and participate in the protocol's decentralized infrastructure. The staking mechanism ensures relayer accountability through automatic deactivation.

***

## 中文

Voidify 使用透明、无需许可的手续费结构，用于维持协议、支持贡献者参与并促进用户隐私，同时不引入托管风险或中心化收费。

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2F29p8GK5zXCWfQawWGaEe%2Fvoidify%20fees.png?alt=media&#x26;token=d14cf7b1-72f5-4751-8761-469ee9a8bd6e" alt="" width="250"><figcaption></figcaption></figure>

***

#### **手续费拆解**

#### 两种提款模式

Voidify 支持两种提款路径，每种都有不同的手续费模型：

**1. Relayer Withdraw（通过已注册 relayer）**

用户通过已注册 relayer 提交提款请求，从而保护隐私，并且不要求收款人支付 gas。

* **Relayer Fee**：由每个 relayer 单独设置（默认 0.1%，最高 10%。费率会影响 relayer 的随机选择顺序）。这部分 SOL 直接给 relayer。
* **DAO Refund Fee**：由 DAO authority 设置（默认 0.3%，最高 10%）。等值 SOL 支付给 relayer，而对应代币价值从 relayer 的质押中扣除并发送到 DAO treasury（staking 上线后会改为发送给 stakers）。
* **收款人收到**：存款金额减去两项手续费。

**2. Direct Withdraw（无 relayer，仅在所有 relayer 不可用时使用）**

用户不通过 relayer 直接提款，并自行支付 gas。

* **Relayer Fee**：始终为 0（没有 relayer 参与）
* **DAO Fee**：由 DAO authority 设置（默认 5%，最高 10%）。这部分 SOL 发送到 DAO treasury（staking 上线后会改为发送给 stakers）。
* **收款人收到**：存款金额减去 DAO fee。

***

### ∅ Token Utility

∅ token 是 Voidify 协议中的 **relayer staking token**。参与 relayer 并从处理提款中赚取费用必须使用它。

#### 对 Relayers（∅ Token Holders）

* ✅ 通过质押 ∅ tokens **注册为 relayer**
* ✅ 从处理的每笔提款中 **赚取 SOL**
* ✅ **设置自定义手续费率**（最高 10%）
* ✅ **管理你的 relayer**（增加质押、更新手续费、更新服务 URL）
* ✅ **贡献去中心化隐私基础设施**

完整的注册、经济模型和运营细节请参阅专门的 **Relayer Documentation**。

***

#### **为什么采用这种模型？**

该模型旨在：

* **激励 relayer 增长**：relayer 从处理的每笔提款中赚取 SOL，形成竞争市场
* **维持协议**：DAO fees 为持续开发提供资金
* **确保 relayer 责任约束**：staking 机制抑制恶意行为
* **保持去中心化**：任何人都可以成为 relayer；手续费率由市场驱动

***

### Fee Architecture

* 所有手续费都通过智能合约逻辑**自动计算并执行**
* 手续费参数在链上验证，ZK proof 会承诺确切手续费金额
* Token-to-SOL conversion 使用 **oracle** 实时报价
* 不存在托管控制或手动手续费路由
* 所有配置变更都需要 **DAO authority** 签名

***

### Summary

∅ token 是 Voidify 中的 **relayer staking token**。它让持有人能够注册 relayer、通过处理提款赚取 SOL，并参与协议的去中心化基础设施。staking 机制通过自动停用确保 relayer 的责任约束。

## Русский

Voidify использует прозрачную permissionless структуру комиссий, предназначенную для поддержки протокола, участия contributors и приватности пользователей — без custodial risk или централизованного сбора комиссий.

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2F29p8GK5zXCWfQawWGaEe%2Fvoidify%20fees.png?alt=media&#x26;token=d14cf7b1-72f5-4751-8761-469ee9a8bd6e" alt="" width="250"><figcaption></figcaption></figure>

***

#### **Fee Breakdown**

#### Two Withdrawal Modes

Voidify поддерживает два пути вывода, каждый со своей моделью комиссий:

**1. Relayer Withdraw (через зарегистрированного relayer)**

Пользователи отправляют запросы на вывод через зарегистрированного relayer, сохраняя приватность и не требуя от получателя платить gas.

* **Relayer Fee**: устанавливается каждым relayer индивидуально (по умолчанию 0.1%, максимум 10%; уровень fee влияет на случайный порядок выбора relayer). Эти SOL идут напрямую relayer.
* **DAO Refund Fee**: устанавливается DAO authority (по умолчанию 0.3%, максимум 10%). SOL-эквивалент идет relayer, а token equivalent списывается из stake relayer и отправляется в DAO treasury (после запуска staking будет отправляться stakers).
* **Получатель получает**: сумму депозита минус обе комиссии.

**2. Direct Withdraw (без relayer; используйте только когда все relayer недоступны)**

Пользователь выводит напрямую без relayer и сам платит gas.

* **Relayer Fee**: всегда 0 (relayer не участвует)
* **DAO Fee**: устанавливается DAO authority (по умолчанию 5%, максимум 10%). Эти SOL идут в DAO treasury (после запуска staking будут отправляться stakers).
* **Получатель получает**: сумму депозита минус DAO fee.

***

### ∅ Token Utility

∅ token служит **relayer staking token** в протоколе Voidify. Он необходим для участия в качестве relayer и заработка комиссий за обработку выводов.

#### Для Relayers (∅ Token Holders)

* ✅ **Зарегистрироваться как relayer**, застейкав ∅ tokens
* ✅ **Зарабатывать SOL** с каждого обработанного вывода
* ✅ **Устанавливать custom fee rates** (до 10%)
* ✅ **Управлять relayer** (добавлять stake, обновлять fees, обновлять service URL)
* ✅ **Участвовать в decentralized privacy infrastructure**

Полные детали регистрации, экономики и операций см. в отдельной **Relayer Documentation**.

***

#### **Почему эта модель?**

Модель предназначена для:

* **Стимулирования роста relayer** — relayer зарабатывают SOL с каждого обработанного вывода, создавая конкурентный рынок
* **Поддержки протокола** — DAO fees финансируют ongoing development
* **Ответственности relayer** — staking mechanisms сдерживают malicious behavior
* **Децентрализации** — любой может стать relayer; fee rates market-driven

***

### Fee Architecture

* Все fees рассчитываются и исполняются **автономно smart contract logic**
* Fee parameters проверяются on-chain — ZK proof commits к точным fee amounts
* Token-to-SOL conversion использует **oracle** для real-time pricing
* Нет custodial control или manual fee routing
* Все configuration changes требуют подписи **DAO authority**

***

### Summary

∅ token — это **relayer staking token** в Voidify. Он позволяет holders регистрироваться как relayer, зарабатывать SOL за обработку выводов и участвовать в decentralized infrastructure протокола. Staking mechanism обеспечивает ответственность relayer через automatic deactivation.

## 日本語

Voidify は、プロトコル維持、contributor participation、ユーザープライバシーを支えるために設計された、透明で permissionless な fee structure を使います。custodial risk や centralized fee collection は導入しません。

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2F29p8GK5zXCWfQawWGaEe%2Fvoidify%20fees.png?alt=media&#x26;token=d14cf7b1-72f5-4751-8761-469ee9a8bd6e" alt="" width="250"><figcaption></figcaption></figure>

***

#### **Fee Breakdown**

#### Two Withdrawal Modes

Voidify は 2 種類の出金経路をサポートし、それぞれ異なる fee model を持ちます。

**1. Relayer Withdraw（登録済み relayer 経由）**

ユーザーは登録済み relayer を通じて出金リクエストを送信し、受取人が gas を払う必要なくプライバシーを維持します。

* **Relayer Fee**：各 relayer が個別に設定します（デフォルト 0.1%、最大 10%。fee level は relayer の random selection order に影響します）。この SOL は relayer に直接渡ります。
* **DAO Refund Fee**：DAO authority が設定します（デフォルト 0.3%、最大 10%）。SOL equivalent は relayer に渡り、token equivalent は relayer の stake から差し引かれて DAO treasury に送られます（staking が live になると stakers に送られるよう変更されます）。
* **Recipient receives**：deposit amount から両方の fees を差し引いた額。

**2. Direct Withdraw（relayer なし。すべての relayer が利用不能な場合のみ使用）**

ユーザーは relayer なしで直接出金し、自分で gas を支払います。

* **Relayer Fee**：常に 0（relayer 不在）
* **DAO Fee**：DAO authority が設定します（デフォルト 5%、最大 10%）。この SOL は DAO treasury に送られます（staking が live になると stakers に送られるよう変更されます）。
* **Recipient receives**：deposit amount から DAO fee を差し引いた額。

***

### ∅ Token Utility

∅ token は Voidify protocol 内の **relayer staking token** です。Relayer として参加し、出金処理から fees を得るために必要です。

#### Relayers（∅ Token Holders）向け

* ✅ ∅ tokens を stake して **relayer として登録**
* ✅ 処理した各 withdrawal から **SOL を獲得**
* ✅ **custom fee rates** を設定（最大 10%）
* ✅ **relayer を管理**（stake 追加、fees 更新、service URL 更新）
* ✅ **decentralized privacy infrastructure** に貢献

登録、経済性、運用の詳細は専用の **Relayer Documentation** を参照してください。

***

#### **なぜこのモデルか？**

このモデルは以下を目的としています。

* **relayer growth の促進**：relayer は処理した各 withdrawal から SOL を得て、競争的な marketplace を作ります
* **protocol の維持**：DAO fees が ongoing development を支えます
* **relayer accountability の確保**：staking mechanisms が malicious behavior を抑制します
* **decentralization の維持**：誰でも relayer になれ、fee rates は market-driven です

***

### Fee Architecture

* すべての fees は **smart contract logic により自律的に計算・実行**されます
* Fee parameters は on-chain で検証されます。ZK proof は正確な fee amounts に commit します
* Token-to-SOL conversion は real-time pricing のため **oracle** を使います
* custodial control や manual fee routing はありません
* すべての configuration changes には **DAO authority** signature が必要です

***

### Summary

∅ token は Voidify 内の **relayer staking token** です。Holders は relayer として登録し、withdrawals 処理から SOL を得て、プロトコルの decentralized infrastructure に参加できます。Staking mechanism は automatic deactivation により relayer accountability を保証します。
