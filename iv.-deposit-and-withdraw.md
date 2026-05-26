---
description: How to Deposit & Withdraw Using Voidify
---

# IV. Deposit & Withdraw

Voidify allows users to deposit fixed-denomination assets into privacy pools and later withdraw them with zero-knowledge proofs. This process creates unlinkability between addresses — but users must follow best practices to preserve their privacy.

#### **Deposit Guide**

**1. Connect Your Wallet**

Click **Connect** and choose a Solana-compatible wallet such as:

* ✅ Phantom
* ✅ Solflare
* ✅ Metamask

Ensure you're connected to **Solana Mainnet**.

***

**2. Select a Token & Amount**

Choose the token you want to deposit (**SOL**) and the corresponding **fixed-denomination pool** (e.g., 1 SOL, 10 SOL,).

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Standardized pool sizes help protect privacy by eliminating unique transaction fingerprints.
{% endhint %}

***

**3. Generate and Secure Your Note**

Click deposit:

* A **private note** will be generated in your browser.
* This note proves you deposited — and is required to withdraw later.

<figure><img src=".gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

> ⚠️ **Important**: Save your note securely.\
> Voidify does not store it. If you lose it, your funds are irrecoverable.

**Do not store notes in:**

* Unencrypted devices
* Browsers or autofill
* Cloud storage or chat apps

***

**4. Confirm Deposit**

Once you've saved the note:

* Click **Confirm**
* Approve the transaction in your wallet
* Your funds will be added to the on-chain privacy pool

***

**5. Wait to Strengthen Privacy**

Withdrawing immediately weakens your anonymity.\
To increase your privacy:

* Wait for more users to deposit into the same pool
* Larger **anonymity sets** reduce correlation risk

You’ll be able to monitor pool activity in the **Anonymity Set Dashboard**.

***

#### **Withdraw Guide**

**1. Connect Wallet & Select Pool**\
Click **Connect** → Choose your wallet → Navigate to the **Withdraw** tab.

***

**2. Paste Your Private Note and Recipient Address**\
Paste your saved note and recipient address into the withdrawal field.

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

> This cryptographically proves you made a deposit — without revealing which one.

***

**3. Choose a Relayer (opeitonal, Because the system will automatically choose)**&#x20;

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

* Select a **relayer** to submit the withdrawal transaction on your behalf

***

**4. Click Withdraw**

* **Click Withdraw**
* Click **Confirm**

<figure><img src=".gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

> The funds will be sent to your selected address without any visible on-chain link to your deposit.

***

**Optional: Note Account (Coming Soon)**

Voidify is building a secure **on-chain backup feature** called the **Note Account**.\
This will allow you to store encrypted notes without relying on off-chain tools.

> ⚠️ Use caution: if your backup key is ever compromised, your deposits can be deanonymized.\
> Only use this feature if you fully understand the tradeoffs.

***

**Never Share Your Note**

Your private note is your key to withdraw funds.\
If anyone accesses it, they can withdraw your deposit.

* ❌ Don’t screenshot it
* ❌ Don’t store in cloud apps
* ❌ Don’t paste in browsers or shared devices

> Losing your note = permanent loss of access.

***

#### Summary

* Use a supported Solana wallet
* Choose a fixed pool size
* Save your private note securely
* Wait for other users to deposit before withdrawing
* Use a relayer to protect your withdrawal identity
* Never reuse wallets
* Never share your private note

Voidify gives you cryptographic privacy.\
Protecting it is your responsibility.
