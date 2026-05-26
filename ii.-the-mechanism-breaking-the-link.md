---
description: How Voidify Works
---

# II. The Mechanism: Breaking the Link

At the core of Voidify’s design are zero-knowledge proofs (zk-SNARKs) and zk-optimized hash functions built to suit Solana’s high-throughput architecture.

<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2FMDD8YhvhqGpVn2jmw9pd%2Fvoidify%20astronaut.png?alt=media&#x26;token=f48c2cea-4c25-4fed-98af-29b956398485" alt="" width="275"><figcaption></figcaption></figure>

***

### Anonymity Pools

Voidify pools are fixed-denomination privacy pools. Each pool accepts one standard deposit amount, such as 0.1 SOL, 1 SOL, or 10 SOL.

A user first deposits into a pool and receives a private note. Later, the user can withdraw the same denomination to a different wallet by generating a zero-knowledge proof. The proof shows that the user owns one valid, unused deposit in the pool, without revealing which deposit it was.

#### Why deposit count matters

More deposits in the same pool create more possible sources for each withdrawal. If a pool has only a few deposits, an observer has fewer candidates to analyze. If a pool has many independent deposits, each withdrawal becomes harder to link to a specific deposit.

For this reason, popular denominations usually provide stronger practical privacy than rarely used denominations.

#### Why timing matters

The time between deposit and withdrawal also affects privacy.

If a user deposits and withdraws shortly afterward, especially when few other deposits happen in between, the withdrawal may be easier to correlate with the recent deposit. Waiting longer allows more deposits to enter the same pool, increasing the number of plausible sources.

A longer delay does not guarantee perfect privacy, but immediate withdrawals usually provide weaker privacy because they create a clearer timing pattern.

***

#### **How Deposits Work**

When a user deposits tokens into Voidify:

* A **private note** is generated, containing two random values: a **secret** and a **nullifier**.
* These values are hashed together using the **Poseidon** hash function, creating a **commitment**.
* This commitment is added as a leaf to a Merkle tree stored on-chain.
* The user must store the private note securely, as it will be required to withdraw later.

***

#### **How Withdrawals Work**

To withdraw from the pool:

* The user generates a **zk-proof** that they know a valid, unused commitment in the Merkle tree.
* A **nullifier hash** is submitted, ensuring the commitment cannot be spent twice.
* The smart contract verifies the zk-proof and nullifier.
* If valid, the contract releases the funds to the recipient address.

Since the proof reveals no information about the original commitment’s position in the Merkle tree, and the nullifier cannot be linked back to the deposit, the source of funds remains private.

***

#### **Zero-Knowledge Proofs (zk-Proofs)**

Voidify uses **zk-SNARKs** — succinct, non-interactive cryptographic proofs that verify claims without revealing the underlying data.

* **Privacy**: Proves ownership of a deposit without revealing which one.
* **Security**: Prevents double-spending through nullifier tracking.
* **Efficiency**: Proofs are generated off-chain and verified on-chain.

***

#### ⚙**Poseidon Hash: Optimized for zk-Proofs on Solana**

Voidify uses the **Poseidon hash** instead of older hash functions like Pedersen. This switch dramatically improves performance on Solana:

| Feature                | Pedersen Hash        | Poseidon Hash        |
| ---------------------- | -------------------- | -------------------- |
| zk-Proof Efficiency    | High constraint cost | Minimal constraints  |
| Compatibility          | EVM-optimized        | zk-circuit optimized |
| Cost & Latency         | Expensive            | Fast & cheap         |
| Suitability for Solana | Poor                 | Excellent            |

**Why Poseidon Hash Matters:**

* Reduced computation = faster proof generation
* Optimized for Solana’s low-latency execution
* Lower contract execution cost
* Maintains strong zk-security guarantees

***

#### **Privacy Tips**

To enhance your privacy:

* Use **relayers** to hide your withdrawal origin
* Wait for additional deposits before withdrawing to increase your anonymity set
* Never reuse notes or expose secret values
* Consider different gas parameters and timing for transactions

***

#### **Summary**

Voidify allows you to transact privately on Solana by combining:

* Zero-knowledge cryptography (zk-SNARKs)
* ZK-optimized hashing (Poseidon)
* High-speed, low-cost smart contracts
* A fully self-custodial architecture

The protocol empowers users to move assets without revealing their activity — giving them privacy without compromising security or decentralization.
