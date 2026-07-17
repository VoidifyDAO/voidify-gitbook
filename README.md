---
description: Introduction to the Voidifesto
---

# I. Premise: Why Privacy Must Exist

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

![](.gitbook/assets/image)

Voidify is a decentralized, non-custodial protocol built on the Solana blockchain. It enables users to deposit and later withdraw crypto assets using zero-knowledge proofs, creating unlinkable transactions between wallets — without relying on any intermediary.

While Solana offers speed and low transaction costs, it lacks native privacy. Every transaction is publicly visible, exposing user activity and compromising confidentiality. Voidify addresses this gap primarily through the flexible-amount [Nova Privacy Pool](iii.-nova-privacy-pool.md), while fixed-denomination Classic pools remain available as an alternative. Both let users withdraw to another wallet without leaving a visible on-chain link to the source deposit.

Nova removes the need to wait for another deposit of the exact same denomination. Different deposit sizes can participate in the same token pool, and large balances can be withdrawn in parts while the remainder stays private.

Voidify leverages Solana’s performance with modern zero-knowledge cryptography to support efficient, shielded value transfer. Built natively in Rust, the protocol integrates zk-proving systems and a frontend designed for self-custodial interaction — all without compromising decentralization or user control.

***

## 中文

![](.gitbook/assets/image)

Voidify 是构建在 Solana 区块链上的去中心化、非托管协议。它让用户能够存入加密资产，并在之后使用零知识证明提款，从而在不同钱包之间创建不可关联的交易，而且不依赖任何中介。

Solana 提供了速度和低交易成本，但它没有原生隐私。每一笔交易都是公开可见的，这会暴露用户活动并损害机密性。Voidify 主要通过灵活金额的 [Nova 隐私池](iii.-nova-privacy-pool.md) 弥补这一缺口，同时保留固定面额 Classic 池作为备选。两种模式都允许用户把资金提取到另一个钱包，而不留下与来源存款之间的可见链上链接。

Nova 消除了等待完全相同面额存款的限制。不同金额可以参与同一个代币池，大额余额也能按需分批提取，并让剩余资金继续保持私密。

Voidify 将 Solana 的性能与现代零知识密码学结合，用于支持高效、受保护的价值转移。协议以 Rust 原生构建，集成 zk 证明系统，并提供面向自托管交互的前端，同时不牺牲去中心化或用户控制权.

## Русский

![](.gitbook/assets/image)

Voidify — это децентрализованный некастодиальный протокол, построенный на блокчейне Solana. Он позволяет пользователям вносить криптоактивы и позже выводить их с помощью доказательств с нулевым разглашением, создавая несвязываемые транзакции между кошельками без посредников.

Solana обеспечивает высокую скорость и низкие транзакционные издержки, но не имеет встроенной приватности. Каждая транзакция публично видима, раскрывает активность пользователя и подрывает конфиденциальность. Voidify решает эту проблему прежде всего через [Nova Privacy Pool](iii.-nova-privacy-pool.md) с гибкими суммами, сохраняя Classic pools с фиксированными номиналами как альтернативу. Оба режима позволяют вывести средства на другой кошелек без видимой ончейн-связи с исходным депозитом.

Nova устраняет необходимость ждать депозит того же номинала. Разные суммы участвуют в одном token pool, а крупный баланс можно выводить частями, сохраняя остаток приватным.

Voidify использует производительность Solana вместе с современной криптографией нулевого разглашения для эффективного защищенного переноса стоимости. Протокол нативно построен на Rust, интегрирует zk-proving systems и фронтенд для самостоятельного хранения средств, не жертвуя децентрализацией или пользовательским контролем.

## 日本語

![](.gitbook/assets/image)

Voidify は Solana ブロックチェーン上に構築された、分散型かつノンカストディアルなプロトコルです。ユーザーは暗号資産を預け入れ、後からゼロ知識証明を使って出金できます。これにより、仲介者に依存せず、ウォレット間の取引を関連付け不能にします。

Solana は高速で取引コストが低い一方、ネイティブなプライバシーはありません。すべての取引は公開され、ユーザーの活動を露出し、機密性を損ないます。Voidify は主に柔軟な金額の [Nova Privacy Pool](iii.-nova-privacy-pool.md) でこの欠落を補い、固定額の Classic pools は代替として維持します。どちらも、元の deposit との明確なオンチェーンリンクを残さず別の wallet へ withdraw できます。

Nova では、完全に同じ額面の deposit を待つ必要がありません。異なる金額が同じ token pool に参加でき、大きな balance も一部ずつ withdraw して残りを private に保てます。

Voidify は Solana の性能と現代的なゼロ知識暗号を活用し、効率的で秘匿された価値移転を支えます。プロトコルは Rust でネイティブに構築され、zk proving systems とセルフカストディ型インタラクション向けフロントエンドを統合しながら、分散性とユーザーのコントロールを損ないません.
