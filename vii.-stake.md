# VII. Stake

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

Staking turns Voidify from a fee-collecting protocol into a community-owned one. It converts the ∅ token from a relayer's collateral into a claim on every withdrawal the network ever processes. The governance rights that come with a stake — proposing, voting, delegating — are described in §VIII; this chapter is about the economics.

### Why Stake

Section III described two protocol revenue streams: a **DAO Refund** paid in VOID by relayers on every relayed withdrawal, and a **DAO Fee** paid in SOL by users on direct withdrawals. The two flows are not symmetric, and staking only intercepts one of them.

* **Relayed withdrawals** are paid for in SOL — the user pays a relayer fee and a DAO Refund, both denominated in SOL, to the relayer who broadcasts the transaction. The protocol then deducts an equivalent amount of VOID from that relayer's staked balance and splits it on-chain by a governance-controlled ratio: one slice flows to the DAO treasury, the remainder flows into the staking reward pool and is distributed pro-rata to stakers. The relayer is made whole by the SOL they received; the staking pool is fed by the VOID that came out of their stake.
* **Direct withdrawals** send their SOL fee in full to the DAO treasury. None of it reaches the staking contract. Direct-withdraw revenue funds the treasury — and through governance, the treasury funds whatever the DAO decides to fund.

The implication for stakers is direct: **every relayed withdrawal on Voidify pays VOID to the people who stake VOID**, in proportion to the share governance has assigned to stakers. Holding the token in a wallet earns nothing. Staking it makes the holder a counterparty to the protocol's relayed-withdrawal revenue.

#### A worked example

Suppose Alice withdraws **10 SOL** through a relayer, at the protocol's default fees:

* **Relayer fee** (0.1%): 0.01 SOL — kept by the relayer.
* **DAO Refund** (0.3%): 0.03 SOL — also paid to the relayer.
* **Alice receives**: 9.96 SOL at her destination address.

The relayer has now earned 0.04 SOL on this single withdrawal. The protocol then deducts **VOID equivalent to 0.03 SOL** — the DAO Refund portion — out of the relayer's staked VOID. Assume governance has set the staker–treasury split to 50/50:

* VOID equivalent to **0.015 SOL** flows to the DAO treasury.
* VOID equivalent to **0.015 SOL** flows into the staking reward pool.

The pool is now richer than it was a moment earlier, and every staker holds a claim on a slice of it proportional to their stake.

Now suppose Bob has **10,000 VOID** staked, and the global stake total is **1,000,000 VOID**. Bob's share is **1%**. Over a week in which Voidify processes thousands of relayed withdrawals and the pool collects, say, **5,000 VOID** in fees, Bob's accrued reward is:

> 1% × 5,000 VOID = **50 VOID**

He can claim those 50 VOID at any time. He can also re-stake them to grow his share — and from then on, every new batch of fees that arrives is divided against the new, larger total. The contract settles his portion automatically whenever he interacts with it, so he never has to time the market or race other claimers.

If, during that week, no one is staked yet, the 5,000 VOID stays in the pool untouched and is paid out to the first stakers when they arrive — the protocol never burns fees on its way to a bookkeeping entry that doesn't exist yet.

### Stake and Unstake

**Staking** transfers VOID from the user into a contract-owned vault, increases the user's recorded balance and the global total, and settles any rewards that had accumulated against their old balance. The first stake also opens the user's account.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Unstaking** is the symmetric operation: VOID returns to the user's wallet, the recorded balance and global total are reduced, and any pending rewards are settled. By default — when the user has not participated in any active governance flow — staking and unstaking are immediate, with no cooldown. A user can never withdraw more than they have staked. Active proposers, voters, and delegators are subject to additional holds; the rules for those holds are introduced in §VIII.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Economic Properties

* **No emission.** The reward pool is fed exclusively by protocol revenue. There is no inflation, no liquidity-mining schedule, no team unlock. Yield is a function of withdrawal volume — and only of withdrawal volume.
* **No minimum.** Any non-zero stake is accepted. Reward share is exactly proportional.
* **No passive lockup.** A holder who stakes for yield alone can withdraw on any block. Holds exist only for active governance participants and only for the duration of their participation.
* **Permissionless rewards.** Anyone — a keeper, a relayer, a curious bystander — can poke the contract to recognize new fees that have arrived in the pool. There is no privileged caller, and no parameter the caller can spoof.

***

## 中文

### 为什么质押？

质押使 VOID 持有人能够参与协议收入分配。通过 relayer 的提款会以 SOL 向 relayer 支付手续费；协议会从 relayer 的质押中扣除与 DAO refund 相等价值的 VOID，并依照治理控制的规则进行分配，其中可包括质押奖励池。

直接提款不同：其配置的 SOL 手续费流向 DAO treasury，不进入质押奖励池。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 示例

对于一笔 `10 SOL` 的 relayer 提款，若 relayer fee 为 `0.1%`、DAO refund 为 `0.3%`：

* Relayer 获得 `0.01 SOL` 的 relayer fee 与 `0.03 SOL` 的 DAO refund。
* 收款人获得 `9.96 SOL`。
* 等值于 `0.03 SOL` 的 VOID 从 relayer 质押中扣除，并按协议分配规则处理。

若治理将其中一部分 VOID 分配给质押者，每位质押者将按其占总质押的比例获得奖励。

### 质押与解除质押

质押会将 VOID 转入合约控制的金库并记录用户份额。解除质押会返还用户可提取的 VOID，并结算已累计奖励。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 特性

* 奖励来自协议收入，而非计划性增发。
* 任何非零质押均可参与。
* 仅为获得奖励而质押的用户通常可立即解除质押；参与活跃治理可能带来锁定限制。
* 奖励结算由链上逻辑执行。

***

## Русский

### Зачем стейкать?

Стейкинг позволяет держателям VOID участвовать в доходах протокола. При выводах через relayer комиссии в SOL выплачиваются relayer; протокол списывает из его стейка эквивалент DAO refund в VOID и распределяет его по правилам, контролируемым управлением, включая пул наград стейкинга.

Прямые выводы устроены иначе: настроенная комиссия в SOL направляется в казначейство DAO и не пополняет пул наград стейкинга.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Пример

Для вывода `10 SOL` через relayer с комиссией relayer `0.1%` и DAO refund `0.3%`:

* Relayer получает `0.01 SOL` как комиссию relayer и `0.03 SOL` как DAO refund.
* Получатель получает `9.96 SOL`.
* Эквивалент `0.03 SOL` в VOID списывается из стейка relayer и распределяется согласно правилам протокола.

Если управление направляет часть этих VOID стейкерам, каждый стейкер получает награды пропорционально своей доле от общего стейка.

### Стейкинг и вывод стейка

Стейкинг переводит VOID в хранилище под контролем контракта и фиксирует долю пользователя. Вывод стейка возвращает доступные VOID пользователю и рассчитывает накопленные награды.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Свойства

* Награды поступают из доходов протокола, а не из запланированной эмиссии.
* Участвовать может любой ненулевой стейк.
* Пользователь, стейкающий только ради наград, обычно может вывести стейк сразу; активное участие в управлении может накладывать ограничения.
* Расчет наград выполняется ончейн-логикой.

***

## 日本語

### なぜステークするのか

ステーキングにより、VOID 保有者はプロトコル収益に参加できます。Relayer 経由の出金では SOL の手数料が relayer に支払われ、プロトコルは DAO refund に相当する VOID を relayer のステークから差し引き、ステーキング報酬プールを含むガバナンス管理の規則に従って配分します。

直接出金は異なり、設定された SOL 手数料は DAO treasury に送られ、ステーキング報酬プールには入りません。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 例

Relayer fee が `0.1%`、DAO refund が `0.3%` の `10 SOL` の relayer 出金の場合：

* Relayer は relayer fee として `0.01 SOL`、DAO refund として `0.03 SOL` を受け取ります。
* 受取人は `9.96 SOL` を受け取ります。
* `0.03 SOL` 相当の VOID が relayer のステークから差し引かれ、プロトコルの配分規則に従って処理されます。

ガバナンスがその VOID の一部をステーカーに配分する場合、各ステーカーは総ステークに占める割合に応じた報酬を受け取ります。

### ステークとアンステーク

ステークでは VOID がコントラクト管理の保管庫へ移され、ユーザーの持分が記録されます。アンステークでは利用可能な VOID がユーザーへ返却され、累積報酬が精算されます。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 特性

* 報酬は予定された新規発行ではなく、プロトコル収益から生じます。
* 0 より大きい任意のステークが参加できます。
* 報酬目的のみでステークするユーザーは通常、直ちにアンステークできますが、ガバナンスへ積極的に参加している場合は制限が生じることがあります。
* 報酬計算はオンチェーンロジックで実行されます。
