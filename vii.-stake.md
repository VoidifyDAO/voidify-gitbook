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

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

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

质押将 Voidify 从一个收取费用的协议，转变为一个由社区拥有的协议。它把 ∅ token 从 relayer 的抵押品，转化为对网络未来处理的每一次提款的收益索取权。质押带来的治理权利（提案、投票、委托）将在 §VIII 中说明；本章讨论的是经济机制。

### 为什么质押

第三章介绍了协议的两类收入流：relayer 在每次 relayed withdrawal 中用 VOID 支付的 **DAO Refund**，以及用户在 direct withdrawal 中用 SOL 支付的 **DAO Fee**。这两条流并不对称，质押只截取其中一条。

* **Relayed withdrawals** 以 SOL 支付：用户向广播交易的 relayer 支付 relayer fee 和 DAO Refund，两者都以 SOL 计价。随后协议从该 relayer 的质押余额中扣除等值 VOID，并按照治理控制的比例在链上拆分：一部分流向 DAO treasury，剩余部分流入 staking reward pool，并按比例分配给 stakers。Relayer 通过收到的 SOL 得到补偿；staking pool 则由从其 stake 中扣出的 VOID 提供资金。
* **Direct withdrawals** 会把 SOL fee 全额发送到 DAO treasury。它不会进入 staking contract。Direct-withdraw revenue 为 treasury 提供资金，并通过治理资助 DAO 决定资助的事项。

对 stakers 的含义很直接：**Voidify 上每一次 relayed withdrawal 都会按治理分配给 stakers 的份额，向质押 VOID 的人支付 VOID**。把 token 放在钱包里不会产生收益。质押它，则使持有人成为协议 relayed-withdrawal revenue 的交易对手。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### 一个具体示例

假设 Alice 通过 relayer 提取 **10 SOL**，并使用协议默认费用：

* **Relayer fee**（0.1%）：0.01 SOL，由 relayer 保留。
* **DAO Refund**（0.3%）：0.03 SOL，也支付给 relayer。
* **Alice receives**：在目标地址收到 9.96 SOL。

Relayer 在这一笔提款中获得了 0.04 SOL。随后协议从 relayer 的 staked VOID 中扣除**等值于 0.03 SOL 的 VOID**，也就是 DAO Refund 部分。假设治理将 staker–treasury split 设为 50/50：

* 等值 **0.015 SOL** 的 VOID 流向 DAO treasury。
* 等值 **0.015 SOL** 的 VOID 流入 staking reward pool。

这个 pool 比刚才更富有了，每个 staker 都按其 stake 比例拥有其中一部分索取权。

现在假设 Bob 质押了 **10,000 VOID**，全局质押总量为 **1,000,000 VOID**。Bob 的份额是 **1%**。某一周内，Voidify 处理了数千笔 relayed withdrawals，pool 收集了例如 **5,000 VOID** 的费用，则 Bob 累计的奖励为：

> 1% × 5,000 VOID = **50 VOID**

他可以在任何时候领取这 50 VOID。他也可以把它们重新质押，以扩大自己的份额；从那之后，新进入的每一批费用都会按照新的、更大的总量来划分。合约会在他与合约交互时自动结算他的份额，因此他无需择时，也无需和其他 claimers 抢跑。

如果在这一周内还没有任何人质押，那么这 5,000 VOID 会原封不动地留在 pool 中，并在第一批 stakers 到来时支付给他们。协议不会在一个尚不存在的记账条目上烧掉费用。

### 质押与解除质押

**Staking** 会把 VOID 从用户转入合约拥有的 vault，增加用户记录余额和全局总量，并结算基于其旧余额已经累计的奖励。第一次质押还会为用户开立账户。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Unstaking** 是对称操作：VOID 返回用户钱包，记录余额和全局总量减少，任何待领取奖励都会被结算。默认情况下，如果用户没有参与任何活跃治理流程，staking 和 unstaking 都是即时的，没有 cooldown。用户永远不能提取超过其已质押数量的 VOID。活跃的 proposers、voters 和 delegators 会受到额外 hold 规则约束；这些规则将在 §VIII 中介绍。

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 经济属性

* **无增发。** Reward pool 完全由协议收入提供资金。没有通胀、没有 liquidity-mining schedule、没有团队解锁。收益是提款量的函数，并且只取决于提款量。
* **无最低门槛。** 任何非零 stake 都可以接受。奖励份额严格按比例计算。
* **无被动锁仓。** 仅为了收益而质押的持有人可以在任何区块退出。Hold 只适用于活跃治理参与者，并且只在参与期间存在。
* **无需许可的奖励。** 任何人（keeper、relayer、好奇的旁观者）都可以触发合约识别 pool 中新到达的费用。没有特权调用者，也没有调用者可以伪造的参数。

***

## Русский

Стейкинг превращает Voidify из протокола, который просто собирает комиссии, в протокол, принадлежащий сообществу. Он превращает ∅ token из залога relayer в право требования на каждый вывод, который сеть когда-либо обработает. Права управления, связанные со стейком — создание предложений, голосование, делегирование — описаны в §VIII; эта глава посвящена экономике.

### Зачем стейкать

В разделе III были описаны два потока дохода протокола: **DAO Refund**, выплачиваемый relayer в VOID при каждом relayed withdrawal, и **DAO Fee**, выплачиваемый пользователями в SOL при direct withdrawal. Эти два потока не симметричны, и стейкинг перехватывает только один из них.

* **Relayed withdrawals** оплачиваются в SOL: пользователь платит relayer fee и DAO Refund, оба номинированы в SOL, relayer, который транслирует транзакцию. Затем протокол списывает эквивалентную сумму VOID из стейкнутого баланса этого relayer и делит ее ончейн по коэффициенту, контролируемому управлением: одна часть идет в DAO treasury, остаток поступает в staking reward pool и распределяется pro-rata между stakers. Relayer компенсируется полученными SOL; staking pool пополняется VOID, вышедшими из его stake.
* **Direct withdrawals** отправляют свою SOL fee полностью в DAO treasury. Она не попадает в staking contract. Доход от direct-withdraw финансирует treasury, а через governance treasury финансирует то, что DAO решит финансировать.

Следствие для stakers прямое: **каждый relayed withdrawal в Voidify платит VOID тем, кто стейкает VOID**, в пропорции к доле, которую governance назначило stakers. Хранение token в кошельке ничего не приносит. Стейкинг делает держателя контрагентом дохода протокола от relayed-withdrawal.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Рабочий пример

Предположим, Alice выводит **10 SOL** через relayer при стандартных комиссиях протокола:

* **Relayer fee** (0.1%): 0.01 SOL — остается у relayer.
* **DAO Refund** (0.3%): 0.03 SOL — также выплачивается relayer.
* **Alice receives**: 9.96 SOL на адрес назначения.

Relayer заработал 0.04 SOL на этом одном выводе. Затем протокол списывает **VOID, эквивалентные 0.03 SOL**, то есть часть DAO Refund, из staked VOID relayer. Предположим, governance установило разделение staker–treasury 50/50:

* VOID, эквивалентные **0.015 SOL**, идут в DAO treasury.
* VOID, эквивалентные **0.015 SOL**, поступают в staking reward pool.

Теперь pool стал богаче, чем мгновение назад, и каждый staker имеет право на его долю пропорционально своему stake.

Теперь предположим, что Bob застейкал **10,000 VOID**, а общий глобальный stake равен **1,000,000 VOID**. Доля Bob составляет **1%**. За неделю, в течение которой Voidify обрабатывает тысячи relayed withdrawals и pool собирает, скажем, **5,000 VOID** комиссий, начисленная награда Bob равна:

> 1% × 5,000 VOID = **50 VOID**

Он может забрать эти 50 VOID в любое время. Он также может снова застейкать их, чтобы увеличить свою долю, и с этого момента каждая новая партия комиссий будет делиться уже относительно нового, большего общего объема. Контракт автоматически рассчитывает его часть при каждом взаимодействии, поэтому ему не нужно угадывать момент рынка или соревноваться с другими claimers.

Если в течение этой недели еще никто не стейкает, 5,000 VOID остаются в pool нетронутыми и выплачиваются первым stakers, когда они появятся. Протокол никогда не сжигает комиссии по пути к бухгалтерской записи, которой еще не существует.

### Stake and Unstake

**Staking** переводит VOID от пользователя в vault, принадлежащий контракту, увеличивает записанный баланс пользователя и общий глобальный объем, а также рассчитывает все награды, накопленные относительно его старого баланса. Первый stake также открывает аккаунт пользователя.

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Unstaking** — симметричная операция: VOID возвращаются в кошелек пользователя, записанный баланс и общий глобальный объем уменьшаются, а все ожидающие награды рассчитываются. По умолчанию, если пользователь не участвовал ни в каком активном governance-процессе, staking и unstaking выполняются сразу, без cooldown. Пользователь никогда не может вывести больше, чем застейкал. Активные proposers, voters и delegators подлежат дополнительным holds; правила этих holds вводятся в §VIII.

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### Экономические свойства

* **Нет эмиссии.** Reward pool питается исключительно доходами протокола. Нет инфляции, нет графика liquidity-mining, нет team unlock. Доходность является функцией объема выводов и только объема выводов.
* **Нет минимума.** Принимается любой ненулевой stake. Доля наград строго пропорциональна.
* **Нет пассивной блокировки.** Держатель, который стейкает только ради доходности, может выйти на любом блоке. Holds существуют только для активных участников governance и только на время их участия.
* **Permissionless rewards.** Любой — keeper, relayer, любопытный наблюдатель — может вызвать контракт, чтобы он распознал новые комиссии, пришедшие в pool. Нет привилегированного caller и нет параметра, который caller может подделать.

***

## 日本語

ステーキングは、Voidify を単なる手数料徴収プロトコルから、コミュニティ所有のプロトコルへ変えます。これにより ∅ token は relayer の担保から、ネットワークが今後処理するすべての出金に対する請求権へと変わります。Stake に伴うガバナンス権（提案、投票、委任）は §VIII で説明します。本章では経済性を扱います。

### なぜステークするのか

第 III 章では、プロトコルの 2 つの収益フローを説明しました。Relayed withdrawal ごとに relayer が VOID で支払う **DAO Refund** と、direct withdrawal でユーザーが SOL で支払う **DAO Fee** です。この 2 つのフローは対称ではなく、ステーキングが受け取るのはそのうち 1 つだけです。

* **Relayed withdrawals** は SOL で支払われます。ユーザーは、トランザクションをブロードキャストする relayer に対して、SOL 建ての relayer fee と DAO Refund を支払います。その後プロトコルは、その relayer の staked balance から等価額の VOID を差し引き、ガバナンスで制御される比率に従ってオンチェーンで分割します。一部は DAO treasury に流れ、残りは staking reward pool に入り、stakers へ pro-rata で分配されます。Relayer は受け取った SOL によって補填され、staking pool はその stake から出た VOID によって供給されます。
* **Direct withdrawals** は SOL fee 全額を DAO treasury へ送ります。これは staking contract には届きません。Direct-withdraw revenue は treasury に資金を供給し、ガバナンスを通じて treasury は DAO が資金提供を決めたものに資金を出します。

Stakers にとっての意味は直接的です。**Voidify 上のすべての relayed withdrawal は、ガバナンスが stakers に割り当てた割合に応じて、VOID をステークしている人に VOID を支払います**。Token をウォレットに保有しているだけでは何も得られません。ステークすることで、保有者はプロトコルの relayed-withdrawal revenue の相手方になります。

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### 具体例

Alice が relayer 経由で **10 SOL** を出金し、プロトコルのデフォルト手数料を使うとします。

* **Relayer fee**（0.1%）：0.01 SOL。Relayer が保持します。
* **DAO Refund**（0.3%）：0.03 SOL。これも relayer に支払われます。
* **Alice receives**：宛先アドレスで 9.96 SOL を受け取ります。

Relayer はこの 1 回の出金で 0.04 SOL を得ました。その後プロトコルは、DAO Refund 部分である**0.03 SOL 相当の VOID** を relayer の staked VOID から差し引きます。Governance が staker–treasury split を 50/50 に設定しているとします。

* **0.015 SOL** 相当の VOID が DAO treasury に流れます。
* **0.015 SOL** 相当の VOID が staking reward pool に流れます。

Pool は直前より豊かになり、すべての staker は自身の stake に比例した取り分を持つことになります。

次に、Bob が **10,000 VOID** をステークしており、global stake total が **1,000,000 VOID** だとします。Bob の share は **1%** です。Voidify が 1 週間で数千件の relayed withdrawals を処理し、pool が例えば **5,000 VOID** の手数料を集めた場合、Bob に発生する報酬は次の通りです。

> 1% × 5,000 VOID = **50 VOID**

Bob はこの 50 VOID をいつでも claim できます。また、再ステークして share を増やすこともできます。その後に入ってくる新しい手数料の各バッチは、新しい、より大きな合計額に対して分配されます。Contract は Bob が interaction するたびに自動的に取り分を精算するため、タイミングを読んだり、他の claimers と競争したりする必要はありません。

その週にまだ誰もステークしていない場合、5,000 VOID は pool にそのまま残り、最初の stakers が現れたときに支払われます。プロトコルは、まだ存在しない会計項目へ向かう途中で fees を burn することはありません。

### Stake and Unstake

**Staking** は、ユーザーから contract-owned vault へ VOID を移し、ユーザーの recorded balance と global total を増やし、旧 balance に対して蓄積していた rewards を精算します。最初の stake ではユーザーの account も開かれます。

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

**Unstaking** は対称的な操作です。VOID はユーザーの wallet に戻り、recorded balance と global total は減少し、pending rewards は精算されます。デフォルトでは、ユーザーが active governance flow に参加していない場合、staking と unstaking は cooldown なしで即時に実行されます。ユーザーは自分がステークした量を超えて引き出すことはできません。Active proposers、voters、delegators には追加の holds が適用されます。その hold ルールは §VIII で説明します。

<figure><img src=".gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 経済的性質

* **発行なし。** Reward pool はプロトコル収益のみで供給されます。インフレ、liquidity-mining schedule、team unlock はありません。Yield は withdrawal volume の関数であり、withdrawal volume だけに依存します。
* **最低額なし。** 0 より大きい stake はすべて受け入れられます。Reward share は完全に比例します。
* **受動的ロックアップなし。** Yield 目的だけでステークする holder は、任意の block で引き出せます。Holds は active governance participants のみに、その参加期間だけ存在します。
* **Permissionless rewards。** Keeper、relayer、好奇心のある観察者など、誰でも contract に働きかけて pool に到着した新しい fees を認識させることができます。Privileged caller は存在せず、caller が偽装できる parameter もありません。
