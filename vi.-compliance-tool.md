# VI. Compliance tool

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
