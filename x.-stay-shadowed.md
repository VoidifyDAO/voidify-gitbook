---
description: Tips to Remain Anonymous
---

# X. Stay Shadowed

## X. Stay Shadowed

Voidify breaks on-chain links between deposit and withdrawal addresses using zero-knowledge proofs. But true privacy depends not just on protocol design — it also depends on **you**.

Even with perfect on-chain cryptography, your browser, wallet, and behavior can leak identifying data.

This guide helps you avoid common pitfalls and protect your privacy.

***

#### 🧠 Privacy Is a Practice

Voidify handles privacy on-chain. You must protect it off-chain.

Leaked metadata — like IP addresses, RPC usage, browser fingerprints, wallet reuse, and note handling — can void the unlinkability Voidify gives you.

***

#### 🌐 Use Privacy-Aware Browsers (That Support Solana Wallets)

To use Voidify, you’ll need a browser that supports **Phantom**, **Solflare**, or similar Solana-compatible wallets — without sacrificing your privacy.

**✅ Recommended:**

* **Firefox (Desktop)** — solid privacy controls and works with Phantom.
* **Brave (Desktop)** — Chromium-based with better privacy defaults than Chrome.
* **Safari or Arc (macOS)** — works with Phantom; less privacy-customizable but cleaner than Chrome.

> ❌ Avoid **Google Chrome** — it tracks background activity and leaks session data by default.

***

**📌 Browser Tips:**

* Use **Private/Incognito Mode** for every Voidify session.
* Use a **dedicated browser profile** just for Voidify interactions.
* Clear **cookies, cache, and local storage** after each use.
* Don’t install unnecessary browser extensions — especially ad blockers, password managers, or analytics tools that run in the background.

***

#### 🛡️ Use a VPN (or Tor) — Hide Your IP

Your IP address can be used to correlate transactions, especially by relayers or RPC providers.

* Use a **reputable paid VPN** — avoid free providers that log or sell your data.
* Choose VPNs with **WireGuard** or **OpenVPN** support.
* For stronger anonymity, use **Tor Browser** to access Voidify (when supported).
* Avoid using your regular internet connection during sensitive operations.

***

#### 🔒 Handle Notes With Extreme Care

Your Voidify **note** is both your private withdrawal key and your cryptographic link to the deposit.

* If someone gets your note, they can steal your funds — or deanonymize your transaction.
* Don’t store notes in cloud storage, plain text, or browser memory.
* Use **encrypted password managers** or cold storage.
* Always delete the note after a successful withdrawal.

***

#### 👛 Use Clean Wallets

Using the same wallet for multiple actions (or multiple Voidify interactions) creates traceable links.

* Use **a new wallet for each deposit and each withdrawal.**
* Avoid withdrawing multiple deposits to the same address.
* Use **open-source wallets** like:
  * **Phantom** (with caution)
  * **Solflare**
  * **MetaMask**

> Avoid MetaMask (even with Solana support) unless self-hosted — it uses RPC endpoints like Infura, which log usage and IPs.

***

#### ⌛ Wait to Withdraw — Don’t Rush

If you deposit and withdraw immediately, it's easier to link your actions.

* Wait until other users have deposited after you.
* Monitor the **anonymity set** (coming in Voidify v1 stats dashboard).
* The more activity between your deposit and withdrawal, the better your privacy.

***

#### 🧩 Fragment Large Balances

Big deposits into low-activity pools stand out.

* Break large amounts into **multiple smaller deposits**.
* Use pools with **high volume and frequent activity**.
* Yes, fees may be slightly higher — but your privacy will be significantly stronger.

***

#### 🔁 Rotate Relayers

Relayers help protect your identity by submitting withdrawal transactions on your behalf.

But if you use the **same relayer for every withdrawal**, patterns can form.

* Rotate relayers each time you withdraw.
* Don’t withdraw multiple notes through the same relayer.
* In future versions, you’ll be able to discover new relayers automatically.

***

#### 🧹 Clean Up After Yourself

Data stored in your browser or extension can betray your privacy — even across wallets.

* After each session:
  * Clear **cookies**
  * Clear **localStorage**
  * Clear **cache**
  * Clear **browsing history**
* Use **Incognito Mode** or dedicated, isolated profiles.

***

#### ⛽ Vary Fee Settings

Bots and analytics tools can fingerprint behavior like:

* Gas/compute unit values
* Transaction size
* Slippage parameters

Try not to use default settings every time.

* Add small randomization to gas or compute unit values if possible.
* Don’t copy-paste fee settings between deposit and withdrawal.

***

#### ✅ Final Summary

Voidify gives you cryptographic privacy on-chain — but the rest is up to you.

**Do this every time:**

* Use clean, privacy-respecting browsers
* Use a VPN or Tor
* Isolate your wallets
* Store notes securely
* Rotate relayers
* Clear all browser data
* Don’t rush your withdrawals

> **Privacy is earned through discipline.** Voidify gives you the tools — you supply the practice.
