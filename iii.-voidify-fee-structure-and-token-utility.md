---
description: Voidify Protocol Fees
---

# III. Voidify Fee Structure & Token Utility

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
