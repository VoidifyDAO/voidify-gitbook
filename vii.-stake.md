# VII. Stake

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

### Why Stake?

Staking makes VOID holders participants in protocol revenue. Relayed withdrawals pay fees in SOL to the relayer; the protocol deducts the corresponding DAO refund value in VOID from the relayer's stake and distributes it according to governance-controlled rules, including the staking reward pool.

Direct withdrawals are different: their configured SOL fee flows to the DAO treasury and does not feed the staking reward pool.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Example

For a `10 SOL` relayed withdrawal at a `0.1%` relayer fee and `0.3%` DAO refund:

* The relayer receives `0.01 SOL` as relayer fee and `0.03 SOL` as DAO refund.
* The recipient receives `9.96 SOL`.
* VOID equivalent to `0.03 SOL` is deducted from the relayer's stake and allocated under the protocol split.

If governance allocates part of that VOID to stakers, each staker receives rewards proportional to their share of the total stake.

### Stake and Unstake

Staking transfers VOID into a contract-owned vault and records the user's share. Unstaking returns the user's available VOID and settles accrued rewards.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Properties

* Rewards come from protocol revenue rather than scheduled emissions.
* Any non-zero stake can participate.
* Users staking only for rewards can normally unstake immediately; active governance participation may impose holds.
* Reward accounting is enforced on-chain.

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
