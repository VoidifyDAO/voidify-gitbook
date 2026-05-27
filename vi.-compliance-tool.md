# VI. Compliance tool

[English](#english) | [中文](#中文) | [Русский](#русский) | [日本語](#日本語)

***

## English

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

***

## 中文

## 合规工具

按照区块链的设计，所有交易都是公开可见的，这可能剥夺用户的金融隐私权。任何人都可以查看某个钱包的交易历史、追踪资产流向，并构建出用户链上活动的详细画像。为回应这一结构性问题，Voidify 协议让用户能够通过打破来源地址与目标地址之间的链上联系，重新获得金融隐私。

然而，保护隐私和金融自由不应以必要时无法证明资金合法来源为代价。隐私权包括控制披露哪些信息、以及向谁披露这些信息的权利。

为满足这一需求，Voidify 提供了一个 **Compliance Tool**，让用户可以证明其资金来源。借助每次存款后生成的 Voidify Note，该工具可以基于用于存款和提款的 Solana 地址，生成一份**经过密码学验证的交易历史证明**。

因此，如果你需要证明从 Voidify 池中提取资产的来源，可以使用 Voidify Compliance Tool 生成合规报告。

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## 如何使用合规工具

每次通过 Voidify 存款时，协议都会生成一份唯一的 **Voidify Note**。之后将存入资产提款到提款地址时，需要使用这份 Note。在必要时，同一份 Note 也可以用于生成 **Compliance Report**，证明所提取资产的来源。

要生成 Compliance Report，用户只需将 Voidify Note 输入到 Compliance Tool 的专用输入框中。

报告仅由用户控制的数据和链上可公开验证的信息生成。它不需要任何特权访问、管理员批准或协议级后门。

***

## 提款前

如果 Note **尚未被花费**（也就是资产尚未被提取），Compliance Tool 只会提供与存款相关的信息，包括：

* 存款交易签名；
* 来源地址；
* commitment hash。

Commitment 是为该笔存款生成并提交到 Voidify 智能合约的哈希值，用于在协议内部表示该笔存款。

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

在这个阶段，Compliance Tool 可以证明某笔给定存款来自某个特定来源地址，即使尚未发生提款。

***

## 提款后

如果 Note **已经被花费**（也就是资产已使用该 Note 提取），Compliance Tool 会扩展报告，加入：

* 提款交易签名；
* 目标地址；
* nullifier hash。

Nullifier hash 是提款时提交到链上的公开值，用于证明该 Note 只被花费了一次，并防止双花。

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

在这个阶段，该工具允许用户重新建立原始来源地址与提款目标地址之间的联系，从而证明相关资产的交易历史。

***

## 合规工具的目的

Voidify Compliance Tool 面向合法、由用户主动发起的信息披露场景：用户可能需要证明提款地址中资产的来源。例如：

* 交易所资金来源审查；
* 会计或审计流程；
* 交易对手尽职调查；
* 面向用户的法律或监管询问。

重要的是，Compliance Tool **不会**削弱所有用户的隐私。它不会引入任何主追踪密钥、管理员覆盖权限或全局监控能力。只有持有相关 Note 的用户，才能为该特定存款和提款历史生成报告。

通过这种方式，Voidify 默认保护隐私，同时仍允许用户在需要时证明资金的合法来源。

***

这些信息也可以下载为 PDF 格式，便于发送给任何需要的第三方：<br>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## 总结

Compliance Tool 允许用户在不破坏协议整体隐私保证的前提下，有选择地、自愿地证明资金来源。它不是监控功能，而是用户保护功能：当披露由用户发起并限定在必要范围内时，隐私与合规可以共存。

***

## Русский

## Compliance Tool

По замыслу блокчейна все транзакции публично видимы, что может лишать пользователей права на финансовую приватность. Любой может изучить историю транзакций кошелька, проследить движение активов и составить подробную картину ончейн-активности пользователя. В ответ на эту структурную проблему протокол Voidify позволяет пользователям вернуть финансовую приватность, разрывая ончейн-связь между адресом источника и адресом назначения.

Однако сохранение приватности и финансовой свободы не должно означать невозможность доказать законный источник средств, когда это необходимо. Право на приватность включает право контролировать, какая информация раскрывается и кому она раскрывается.

Для этой цели Voidify включает **Compliance Tool**, который позволяет пользователям доказать происхождение своих средств. Используя Voidify Note, созданную после каждого депозита, инструмент может сформировать **криптографически подтвержденное доказательство истории транзакций** на основе адресов Solana, использованных для депозита и вывода активов.

Поэтому, если вам когда-либо потребуется доказать происхождение активов, выведенных из пула Voidify, вы можете использовать Voidify Compliance Tool для создания compliance report.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## Как использовать Compliance Tool

Каждый раз при депозите через Voidify протокол создает уникальную **Voidify Note**. Эта Note требуется для последующего вывода внесенных активов на адрес вывода. Та же Note при необходимости может использоваться для создания **Compliance Report**, подтверждающего происхождение выведенных активов.

Чтобы создать Compliance Report, пользователю нужно только ввести Voidify Note в специальное поле Compliance Tool.

Отчет создается исключительно из данных, контролируемых пользователем, и публично проверяемой ончейн-информации. Он не требует привилегированного доступа, административного одобрения или протокольного бэкдора.

***

## До вывода

Если Note **еще не была потрачена** (то есть активы еще не были выведены), Compliance Tool предоставляет только информацию, связанную с депозитом, включая:

* подпись транзакции депозита;
* адрес источника;
* commitment hash.

Commitment — это хешированное значение, созданное для депозита и отправленное в смарт-контракт Voidify, чтобы представлять депозит внутри протокола.

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

На этом этапе Compliance Tool может доказать, что конкретный депозит был сделан с определенного адреса источника, даже до какого-либо вывода.

***

## После вывода

Если Note **была потрачена** (то есть активы были выведены с использованием этой Note), Compliance Tool расширяет отчет, добавляя:

* подпись транзакции вывода;
* адрес назначения;
* nullifier hash.

Nullifier hash — это публичное значение, отправляемое ончейн во время вывода, чтобы доказать, что Note была потрачена только один раз, и предотвратить двойную трату.

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

На этом этапе инструмент позволяет пользователю заново установить связь между исходным адресом источника и адресом назначения вывода, тем самым подтверждая историю транзакций соответствующих активов.

***

## Цель Compliance Tool

Voidify Compliance Tool предназначен для законного раскрытия по инициативе пользователя в ситуациях, когда пользователю может потребоваться доказать источник активов, находящихся на адресе вывода. Это может включать, например:

* проверки источника средств на биржах;
* бухгалтерские или аудиторские процедуры;
* due diligence контрагента;
* юридические или регуляторные запросы, адресованные пользователю.

Важно, что Compliance Tool **не** ослабляет приватность всех пользователей. Он не вводит мастер-ключ трассировки, административное переопределение или возможность глобального наблюдения. Только пользователь, владеющий соответствующей Note, может создать отчет для конкретной истории депозита и вывода.

Таким образом, Voidify сохраняет приватность по умолчанию и одновременно позволяет пользователям доказать законный источник средств, когда это необходимо.

***

Эту информацию также можно загрузить в формате PDF, чтобы ее было проще отправить любой нужной третьей стороне:<br>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## Итоги

Compliance Tool позволяет пользователям выборочно и добровольно доказывать происхождение своих средств, не нарушая гарантий приватности протокола в целом. Это не функция наблюдения, а функция защиты пользователя: она обеспечивает сосуществование приватности и compliance, когда раскрытие инициируется пользователем и ограничено необходимым объемом.

***

## 日本語

## Compliance Tool

ブロックチェーンの設計上、すべてのトランザクションは公開されており、これによりユーザーは金融プライバシーを失う可能性があります。誰でもウォレットのトランザクション履歴を調べ、資産の流れを追跡し、ユーザーのオンチェーン活動について詳細な画像を作ることができます。この構造的な問題に対して、Voidify プロトコルは、送金元アドレスと送金先アドレスのオンチェーンリンクを断つことで、ユーザーが金融プライバシーを取り戻せるようにします。

しかし、プライバシーと金融上の自由を守ることは、必要なときに合法的な資金源を示せなくなることを意味してはなりません。プライバシー権には、どの情報を、誰に開示するかをコントロールする権利も含まれます。

この必要性に対応するため、Voidify には **Compliance Tool** が含まれており、ユーザーが資金の出所を証明できるようになっています。各預入後に生成される Voidify Note を使うことで、このツールは資産の預入と出金に使われた Solana アドレスに基づき、**暗号学的に検証されたトランザクション履歴の証明**を発行できます。

したがって、Voidify プールから出金した資産の出所を証明する必要がある場合、Voidify Compliance Tool を使って compliance report を生成できます。

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

***

## Compliance Tool の使い方

Voidify を通じて預入が行われるたびに、プロトコルは一意の **Voidify Note** を生成します。この Note は、後で預け入れた資産を出金アドレスへ引き出すために必要です。同じ Note は、必要に応じて、出金した資産の出所を証明する **Compliance Report** の生成にも使用できます。

Compliance Report を生成するには、ユーザーは Compliance Tool の専用入力欄に Voidify Note を入力するだけです。

レポートは、ユーザーが管理するデータと、オンチェーンで公開検証可能な情報のみから生成されます。特権アクセス、管理者承認、プロトコルレベルのバックドアは必要ありません。

***

## 出金前

Note が**まだ使用されていない**場合（つまり、資産がまだ出金されていない場合）、Compliance Tool は預入に関する情報のみを提供します。これには次が含まれます。

* 預入トランザクションの署名；
* 送金元アドレス；
* commitment hash。

Commitment は、預入のために生成され、プロトコル内でその預入を表すために Voidify スマートコントラクトへ送信されるハッシュ値です。

<figure><img src=".gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

この段階では、Compliance Tool は、出金がまだ発生していなくても、特定の預入が特定の送金元アドレスから行われたことを証明できます。

***

## 出金後

Note が**使用済み**の場合（つまり、その Note を使って資産が出金された場合）、Compliance Tool はレポートを拡張し、次を含めます。

* 出金トランザクションの署名；
* 送金先アドレス；
* nullifier hash。

Nullifier hash は、出金時にオンチェーンで提出される公開値であり、Note が一度だけ使用されたことを証明し、二重使用を防ぐためのものです。

<figure><img src=".gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

この段階では、このツールによりユーザーは元の送金元アドレスと出金先アドレスのリンクを再確立でき、関係する資産のトランザクション履歴を証明できます。

***

## Compliance Tool の目的

Voidify Compliance Tool は、ユーザーが出金アドレスに保有する資産の出所を証明する必要がある状況で、合法的かつユーザー主導の開示を行うために設計されています。例として次が含まれます。

* 取引所による資金源確認；
* 会計または監査手続き；
* 取引相手のデューデリジェンス；
* ユーザーに向けられた法的または規制上の照会。

重要なのは、Compliance Tool がすべてのユーザーのプライバシーを**弱めない**という点です。これはマスター追跡キー、管理者による上書き、またはグローバル監視能力を導入しません。該当する Note を保有するユーザーだけが、その特定の預入と出金履歴に関するレポートを生成できます。

このように、Voidify はデフォルトでプライバシーを保護しながら、必要な場合には合法的な資金源を証明できるようにします。

***

この情報は PDF 形式でもダウンロードでき、必要な第三者へ送付しやすくなります。<br>

<figure><img src=".gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

***

## まとめ

Compliance Tool により、ユーザーはプロトコル全体のプライバシー保証を損なうことなく、自分の資金の出所を選択的かつ自発的に証明できます。これは監視機能ではなく、ユーザー保護機能です。つまり、開示がユーザーによって開始され、必要な範囲に限定される場合、プライバシーとコンプライアンスは共存できます。
