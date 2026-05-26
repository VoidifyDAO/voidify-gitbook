---
description: What Is a Relayer?
---

# V. Voidify Relayers



<figure><img src="https://2312443754-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FDJuzOHtvwNvqd2KgUdyF%2Fuploads%2Fv3iEqigpRTJuuPIJ8jud%2Frelayer.png?alt=media&#x26;token=500d66e1-0211-48ee-9f08-84c50a1edcee" alt="" width="91"><figcaption></figcaption></figure>

Relayers are independent participants within the Voidify protocol who help facilitate privacy-preserving withdrawals. By submitting transactions to the blockchain on behalf of users, relayers prevent withdrawal wallets from being linked to deposit addresses — all without ever accessing user funds or identities.

***

**Key Functions and Guarantees**

* **Privacy-Preserving**: Allows users to withdraw without revealing their own wallet address on-chain
* **Trustless Operation**: Relayers cannot alter, reroute, or access deposited funds — all transaction data is validated by zero-knowledge proofs
* **Gas Support**: Useful when the recipient wallet has no SOL to cover transaction fees
* **Decentralized Network**: The relayer system is open and community-run; protocol developers have no centralized control

{% hint style="info" %}
Relayers are essential to Voidify’s privacy model — acting as anonymous broadcasters to maintain unlinkability between deposit and withdrawal events.
{% endhint %}

**Why Relayers Matter**

Even with zero-knowledge proofs, withdrawing directly from your own wallet exposes your public key on-chain. This reintroduces traceability and erodes privacy.

Relayers solve this by submitting your withdrawal transaction through their own address — unlinking you from both the proof and the transaction broadcast.

***

## ⚙️ How It Works

1. The user generates a zero-knowledge withdrawal proof off-chain
2. The user transmits the proof and request to a relayer via a private channel
3. The relayer broadcasts the transaction from their own address
4. Funds are transferred to the recipient address
5. The relayer receives a protocol-defined fee included in the transaction

Throughout this process, the relayer never knows the origin, identity, or intent of the user — preserving full operational privacy.

***

## 🚀 Becoming a Relayer

### Requirements

To register as a relayer, you must:

* **Stake ∅ tokens**: A minimum stake amount is required for the first time(configurable by DAO, typically 10M ∅ tokens)
* **Provide a unique name**: 3–32 characters, lowercase alphanumeric + hyphen/underscore
* **Provide a service URL**: Your relayer endpoint where users can submit withdrawal requests
* **Set your fee rate**: Choose your relayer fee (max 10%)
* **Server** (2 GB of memory is enough)
* **Stay active**: minimum threshold(configurable by DAO, typically 1M ∅ tokens)

### Registration Process

#### **1. Prepare a Server**

Get a VPS or dedicated server with at least 2 GB RAM. Any Linux distribution works (Ubuntu recommended).

#### **2. Point a Domain to Your Server**

Add a DNS **A record** pointing your domain (e.g. `relayer.example.com`) to your server's public IP address:

| Type | Name    | Value            |
| ---- | ------- | ---------------- |
| A    | relayer | `YOUR_SERVER_IP` |

Wait for DNS propagation (usually a few minutes, up to 24 hours).

#### **3. Install Nginx**

```bash
sudo apt update
sudo apt install -y nginx
```

#### **4. Configure Nginx Reverse Proxy**

Create a config file for your relayer:

```bash
sudo nano /etc/nginx/sites-available/relayer
```

Paste the following (replace `relayer.example.com` with your domain):

```nginx
server {
    listen 80;
    server_name relayer.example.com;

    location / {
        proxy_pass http://127.0.0.1:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable the site and restart Nginx:

```bash
sudo ln -s /etc/nginx/sites-available/relayer /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

#### **5. Enable HTTPS with Certbot**

Install Certbot and obtain a free SSL certificate from Let's Encrypt:

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d relayer.example.com
```

Follow the prompts to complete certificate issuance. Certbot will automatically update your Nginx config to serve HTTPS.

Verify auto-renewal is set up:

```bash
sudo certbot renew --dry-run
```

Your relayer endpoint is now accessible at `https://relayer.example.com`.

#### **6. Download and Configure the Relayer**

Download the latest release from [GitHub Releases](https://github.com/VoidifyCommunity/voidify-relayer/releases):

```bash
wget https://github.com/user-attachments/files/26513398/voidify-relayer-release.zip
unzip voidify-relayer-release.zip
cd voidify-relayer-release
```

Set up the environment:

```bash
cp .env.example .env
```

Edit `.env` and fill in `RELAYER_PRIVATE_KEY` with your Base58-encoded Solana private key.

{% hint style="info" %}
Use the private key of a wallet intended for testing. The code will be open-sourced when it goes live on mainnet
{% endhint %}

#### **7. Run the Relayer**

```bash
# Start in a screen session so it keeps running after you disconnect
screen -S relayer
./voidify-relayer

# Detach from screen: press Ctrl+A then D
# Re-attach later:
screen -r relayer
```

#### **8. Register On-Chain**

Once your relayer service is running and accessible via HTTPS, register on-chain on frontend(voidify.4sol.xyz)\
-> [Twitter video](https://x.com/VoidifyCTO/status/2041206994493935888)

***

## What You Earn

As a registered relayer, you earn:

* **Relayer Fee**: Your custom fee rate (up to 10%) on every withdrawal you process
* **Platform Fee (in SOL)**: You receive the platform's fee portion in SOL upfront
* **Token Deduction**: The platform fee's token equivalent is deducted from your staked ∅ tokens and sent to the DAO treasury

> **Example**: If you process a 10 SOL withdrawal with a 0.1% relayer fee and 0.3% DAO fee:
>
> * You receive: 0.01 SOL (relayer fee) + 0.03 SOL (DAO fee) = **0.04 SOL**
> * Your stake is reduced by: 0.03 SOL worth of ∅ tokens (based on oracle price)
> * User receives: 9.96 SOL

## 🎯 Relayer Selection Mechanism

Voidify implements an intelligent, weighted random selection algorithm to automatically choose the optimal relayer for each withdrawal transaction. This ensures a balance between cost-efficiency, reliability, and decentralization.

### How Relayers Are Selected

When a user initiates a withdrawal, the system:

1. **Filters Active Relayers**: Only considers relayers that are:
   * Registered and active on-chain
   * Passing health checks (responsive API endpoints)
   * Above the minimum stake threshold
2.  **Calculates Selection Weight**: Each relayer receives a score based on:

    ```txt
    Score = StakeAmount × max(0, 1 - 25 × (fee/1000)²)
    ```

    This formula means:

    * **Higher stake** = Higher selection probability (more skin in the game)
    * **Lower fees** = Higher selection probability (better for users)
    * The fee penalty is quadratic, so high-fee relayers are strongly discouraged
3. **Weighted Random Selection**: Relayers are chosen probabilistically based on their scores
   * A relayer with 2x the score has 2x the chance of being selected
   * This prevents monopolization while rewarding quality service

### Selection Examples

**Example 1: Two Relayers**

* Relayer A: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (100/1000)²) = 10,000,000 × 0.75 = 7,500,000
* Relayer B: 5M ∅ stake, 50 bps (0.5%) fee → Score = 5,000,000 × max(0, 1 - 25 × (50/1000)²) = 5,000,000 × 0.9375 = 4,687,500

Selection probability:

* Relayer A: 61.5% chance
* Relayer B: 38.5% chance

**Example 2: Low Fee Advantage**

* Relayer A: 10M ∅ stake, 10 bps (0.1%) fee → Score = 10,000,000 × max(0, 1 - 25 × (10/1000)²) = 10,000,000 × 0.9975 = 9,975,000
* Relayer C: 10M ∅ stake, 100 bps (1%) fee → Score = 10,000,000 × 0.75 = 7,500,000

Selection probability:

* Relayer A: 57% chance (significantly rewarded for lower fee)
* Relayer C: 43% chance

### Benefits of This Approach

✅ **Fair Competition**: New relayers with competitive fees can gain market share&#x20;

✅ **Quality Incentive**: Higher stakes and lower fees are rewarded with more business&#x20;

✅ **Decentralization**: Prevents any single relayer from dominating the network&#x20;

✅ **User Protection**: Automatically favors cost-effective, well-capitalized relayers

✅ **Transparency**: Selection algorithm is open-source and verifiable

### Manual Selection

Users can also manually choose a specific relayer from the interface if they prefer:

* View all active relayers with their fees
* Sort by fee (lowest first) or stake (highest first)
* Select any relayer for their withdrawal

This gives users full control while providing intelligent defaults for convenience.

***

## Relayer Management

Once registered, you can:

* **Add Stake**: Increase your staked ∅ tokens at any time
* **Update Fee**: Change your relayer fee rate (max 10%)
* **Update URL**: Change your service endpoint
* **Monitor Stats**: Track your total withdrawals processed, SOL earned, and tokens deducted

## Deactivation & Reactivation

* If your stake drops below the minimum threshold(default 1M) (due to DAO fee deductions), you are **automatically deactivated**
* You can reactivate by adding more ∅ tokens to bring your stake above the minimum
* Deactivated relayers cannot process new withdrawals until reactivated

## Unregistration

The DAO authority can:

* **Unregister** a relayer: Returns all staked tokens and removes the relayer from the network

<br>
