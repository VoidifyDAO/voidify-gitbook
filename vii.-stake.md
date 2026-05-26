# VII. Stake

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
