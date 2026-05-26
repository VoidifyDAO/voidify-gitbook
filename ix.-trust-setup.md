# IX. Trust setup

A Groth16 proving system is only as honest as the randomness used to set it up. The withdraw circuit at the heart of Voidify — the one that lets a depositor walk away with their SOL without revealing which note they're spending — is verified on-chain against a fixed **verifying key**. Generating that key requires sampling a piece of secret randomness, and **whoever still holds that secret can forge proofs**: they can construct withdrawals that pass on-chain verification against arbitrary nullifiers, minting SOL out of thin air. The job of a trusted setup ceremony is not to ask the world to trust someone with that secret — it is to make sure that **no one** ends up holding all of it.

This chapter describes the public Phase 2 ceremony that produces Voidify's withdraw verifying key, the cryptographic property it relies on, and the artifacts it leaves behind for anyone to audit. Every withdrawal Voidify will ever process is verified on-chain against the keys this ceremony produces. This chapter is how we earn the right to call those keys sound.

### Why a Ceremony

Groth16 splits its setup into two phases. Phase 1 — **Powers of Tau** — is circuit-independent and was performed by the public Perpetual Powers of Tau ceremony with thousands of contributors over multiple years. Voidify reuses one of its publicly archived transcripts; we are not re-running Phase 1.

Phase 2 is **circuit-specific**. Once a circuit (in our case `withdraw.circom`) is compiled to its R1CS form, a fresh round of multi-party computation must mix new randomness with the Phase 1 output to produce the final proving and verifying keys for that exact circuit. This is the round that Voidify is asking the public to participate in.

The security property of Phase 2 is unusual and important: **the resulting verifying key is safe so long as a single contributor was honest and erased their entropy**. Not a majority. Not a quorum. One. Every additional contributor only widens the margin. An attacker who wants to break soundness has to compromise — or be — every single person who ever contributed. By the time this ceremony closes, that target list will not be small.

### How to Contribute

Open the ceremony web app, sign in (GitHub, X, or anonymous), connect a Solana wallet, type a few characters of entropy, and click **Contribute**. Everything cryptographically meaningful happens inside that browser tab. The contributor's secret randomness never leaves the device — it lives only for the duration of one in-browser `snarkjs` call and is gone the moment the tab closes. The published contribution log will then list the wallet address, the optional social handle, and the BLAKE2b-512 hash of the resulting zkey.

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### What Anyone Can Check

The ceremony is run by Voidify, but it is not trusted to Voidify. Three properties make the result independently verifiable:

* **Strict chain extension.** The coordinator only accepts a contribution if it extends the existing chain by exactly one new entry, rooted at the same starting state and matching the existing chain entry-for-entry up to that point. Forking from the public genesis and silently overwriting the live chain is not a path the server will follow.
* **Full transcript is public.** The genesis state, the live chain, every archived contribution, and the log mapping each archive to a wallet address and a file hash are all downloadable throughout the ceremony. An auditor can re-walk the chain at any point and confirm that the published final state is the unique result of the published sequence of contributions.
* **Reproducible contribute UI.** The web app is served as a static bundle pinned to IPFS, and a separate verifier repository — [`voidify-ceremony-verifier-frontend`](https://github.com/VoidifyCommunity/voidify-ceremony-verifier-frontend) — builds the same source and emits the IPFS address it would produce. A contributor who reproduces the build for themselves can confirm that the bundle their browser is about to load is exactly the published source — no injected analytics, no hidden upload path that bypasses the local computation.

The first property closes off backend mischief. The second makes any deviation auditable after the fact. The third extends the same audit to the only piece of code with access to the contributor's secret entropy.

If all three hold, the only remaining trust assumption is the one this whole ceremony exists to soften: that **at least one of the contributors honestly discarded their entropy**. That is the entire residual surface.

### Finalization

When the contribution window closes, a **public-beacon randomness layer** is applied on top of the final chain — typically the hash of a future Bitcoin block, fixed and announced in advance, before its value can be known. The beacon closes the one residual attack the per-contributor model does not close on its own: a contributor who chose their entropy after seeing every transcript before theirs still cannot anticipate a value that did not yet exist when they decided to participate.

The verifying key is then extracted and embedded into the on-chain withdraw verifier by a Solana program redeploy. There is no off-chain switch that swaps the keys quietly: any change to the keys the network verifies against is itself a public on-chain event.

### Why This Is Enough

Every additional contributor adds one more person an attacker would have to compromise — and even one honest participant is sufficient to make the verifying key sound. Contributing requires no token, no KYC, no social account, no special hardware. The browser does the work, the server records the result, and the public log makes the record permanent.

**One honest contributor is enough — and every contribution after the first only widens the margin.**
