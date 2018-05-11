Delegated Proof of Stake:
Features & Tradeoffs
Myles Snider, Kyle Samani, and Tushar Jain?
March 2, 2018? 
。

DPoS（委托权益证明）：特征&利弊

作者：Myles Snider, Kyle Samani, and Tushar Jain?

2018 年 3 月 2 日


Note: Most of this analysis refers to DPoS as implemented in BitShares, Steem, and EOS. Other platforms use a similar DPoS
framework but alter certain features. Much of this analysis will focus specifically on EOS’s consensus algorithm. We will
publish a full analysis and valuation of EOS in the future.?

**摘要**：这些分析大多数分析是指在 BitShares 、 Steem 和 EOS 中实现的 DPoS 。其它平台使用类似的 DPoS 框架，只不过改变某些特性。大部分的分析将专注于EOS的共识算法上。我们将在未来发布对EOS的完整分析和评估。

Introduction
Distributed ledgers don’t easily scale. That fact has become readily apparent in the last few years as
Bitcoin, Ethereum, and others have faced serious challenges as they attempt to increase the speed
and throughput of their platforms.?

引言

分布式账本不容易扩展。在过去几年中，当比特币，以太坊和其它公司尝试在提高平台速度和吞吐量时面临严峻挑战，这一事实在过去几年已经显而易见。

This problem can be best understood as a ?scalability trilemma? (this idea was first formalized by ?Vitalik
Buterin? and ?Trent McConaghy?). The scalability trilemma posits that any blockchain system in which
every node validates every transaction can have only two of three potential properties: decentralization
of block production (DBP), safety, and scalability. These properties can be defined as follows:?

这个问题可以最好地理解为可扩展性三难问题（这个想法首先由 Vitalik Buterin 和 Trent McConaghy 正式确定）。可扩展性三难问题假定每个节点验证每个交易的任何区块链系统可能只有三个潜在属性中的两个：区块产生的去中心化（DBP），安全性和可扩展性。这些属性可以定义如下：

● DBP can be quantified as the number of block producers.
● Safety can be quantified as the cost of mounting a Byzantine attack that affects liveness or
transaction ordering. Note that safety does not refer to the integrity of cryptographic
signatures, or the ability of a 3rd party to derive a set of private keys from public keys.
● Scalability can be quantified as the number of transactions per unit of time that the system can
process.


- DBP可以量化为区块生产者的数量。

- 安全性可以量化为造成影响活跃度或交易顺序的拜占庭攻击的成本。请注意，安全性并不是指加密签名的完整性，也不是指第三方从公钥导出一组私钥的能力。

- 可扩展性可以量化为系统每单位时间可以处理的交易数量。

While projects like ?Ethereum?, ?Dfinity?, ?Polkadot?, and ?Kadena? are attempting to ?solvethe scalability
trilemma via sharding, alternative consensus schemes, and other techniques, we don’t yet have a live platform that has solved this trilemma. Even if one of these projects does manage to solve the
scalability trilemma, the market may not care. It is entirely possible that users are willing to accept
tradeoffs in decentralization of block production or safety in the name of better performance and
easier user experience for certain use cases.?

尽管以太坊，Dfinity ，Polkadot 和 Kadena 等项目试图通过分片，替代性共识方案和其它技术来解决可扩展性问题，但目前我们还没有一个平台解决了这个三难选择。即使这些项目中的某一个确实设法解决了可扩展性的难题，但市场可能并不关注。用户愿意接受区块生产或安全性在去中心的方面进行权衡，以便在特定场景下获取更好的性能和用户体验。


Decentralization is valuable to ensure that any given party cannot alter the database. More
decentralization means it is harder to collude to alter the database. There are different levels of
protection which are necessary for different use cases. Bitcoin, being censorship-resistant money, is
designed for sovereign-grade protection; it is designed to withstand an attack by a large nation-state.
However this isn’t necessary for most decentralized applications (dApps). These dApps need
platform-grade protection; global, neutral databases uncontrolled by any one party. 


去中心化对于确保任何一方不能改变数据库是有价值的。更分散的情况意味着更难共谋改变数据库。不同场景需要不同级别的保护。比特币作为抵制审查的 资金，专为主权级保护而设计；同时，它也为防止大型攻击而设计。然而，这对于大多数分布式应用程序（dApps）来说并不是必需的。这些dApp需要平台级别的保护；全球性的，不受任何一方控制的中立数据库。


Delegated Proof of Stake (DPoS) concentrates block production in the hands of just a few, known,
semi-trusted entities in order to achieve orders of magnitude more scalability than proof-of-work
(PoW) or other proof-of-stake (PoS) blockchains. In this analysis, we’ll examine the features and
tradeoffs of DPoS.

委托权益证明（ DPoS ）集中区块生产在少数已知的部分信任的实体手中，以便实现比工作量证明（PoW）或其它权益证明（PoS）更高数量级的可扩展性区块链。在下面分析中，我们将研究DPoS的功能和利弊。


Delegated Proof of Stake 

Delegated proof of stake (DPoS) is a consensus algorithm invented by Dan Larimer in 2013. DPoS was originally invented to power BitShares, Larimer’s first blockchain project. He refined it in his second
project, Steem, and is refining it further in EOS, which he’s been working on for about one year. While
Larimer invented DPoS and continues to evolve the algorithm, several other projects have adopted
DPoS and made changes. Current blockchains utilizing DPoS include:

DPoS

委托权益证明（ DPoS ）是 Dan Larimer 在 2013 年发明的共识算法。DPoS 最初是为 Larimer 的第一个区块链项目 BitShares 发明的。他在 Steem 项目中完善了它，并在EOS中进一步完善，持续的研究始终没有停止（译者注：EOS众筹这一年也是研究进化的一年）。Larimer发明了DPoS并继续优化该算法，不少项目已采用DPoS并进行了修改。目前使用DPoS的区块链包括：


● EOS, BitShares, Steem, Golos, Ark, Lisk, PeerPlays, Nano (formerly Raiblocks), and Tezos 

● Cosmos/Tendermint, Cardano, and a few others use consensus algorithms loosely based on DPoS


-  EOS, BitShares, Steem, Golos, Ark, Lisk, PeerPlays, Nano (早期称为 Raiblocks)和 Tezos 

- Cosmos / Tendermint，Cardano 和其它一些松散地使用基 DPoS 共识算法

In DPoS, those who hold the network token are able to cast votes to elect block producers; votes are weighted by the voter’s stake, and the block producer candidates that receive the most votes are those who produce blocks. Users can also delegate (“proxy”) their voting power to another user who can vote on their behalf. DPoS is a liquid, representative democracy with token holder suffrage.
DPoS can also be thought of as a formalized, digital version of a traditional organizational hierarchy that operates in a completely transparent way. While there are problems with both democracy and corporate governance that are beyond the scope of this paper, one compelling features of DPoS is that the open-source nature of these protocols means that users can fork if they disagree with the majority. The same cannot be said of democracies, corporations, and other organizational structures. DPoS adopts ideas from many traditional governance models, but is ultimately far more flexible and transparent. 


在DPoS中，持有网络 Token 的人可以投票选举区块生产者（ BP ）；选票的权重取决于选民的权益量，得票最多的区块生产者候选人是生产区块的人。用户也可以委托（“代理”）他们的投票权给另一个可以代表他们投票的用户。DPoS是一种具有代表性的民主，具有象征性的投票权。

DPoS 也可以被认为是传统组织层级的正式数字版本，且以完全透明的方式运作。尽管民主和公司治理方面的问题不在本文讨论的范围，但 DPoS 的一个引人注目的特征是，这些协议的开源特性意味着用户如果不同意大多数人的意见，就可以分叉。民主国家，公司和其他组织结构也是如此。DPoS采纳了许多传统治理模式的想法，但最终更加灵活和透明。


Block producers can be voted in or out at any time, so the threat of loss of income and reputation is one of the major incentives against bad behavior. Additionally, slashing conditions can be implemented in DPoS rather trivially. Most traditional PoS implementations allow users to produce blocks proportional to their stake in the network. DPoS allows users to cast votes proportional to their stake to decide who produces blocks. Block producers themselves do not necessarily need to have a large stake, but they must compete to receive votes from users.

区块打出块人（ BP  ）可以随时进入或退出，但收入和声誉损失的威胁是防止其作恶的主要动机之一。另外，slashing conditions 可以应用于 DPoS。大多数传统的 PoS 允许用户生成与他们在网络中权益成比例的区块。DPoS允许用户投入和其拥有的权益票数以决定谁产生区块。区块块生产者本身不一定需要拥有大量权益（stake），但他们必须竞争以获得用户的投票。

DPoS can power entire blockchains, or it can be used as a consensus algorithm for child chains,sidechains, private blockchains, and more. DPoS could be used to power consensus within Ethereum Plasma chains, and DPoS bears many similarities to the “Proof of Authority” consensus mechanism formalized by Parity. It could also be a solution for application-specific chains like those in Cosmos zones. 
For other in-depth documentation on DPoS, see this link and this link from BitShares, and this white paper from Larimer. 

DPoS 可以为整个区块链提供动力，或者它可以用作子链，侧链，私人区块链等的一致性算法。DPoS 可用于在以太坊 Plasma（可扩展的自主智能合约）链内实现共识，DPoS 与[Parity](https://www.parity.io/)形式化的[“权威证明”](https://github.com/paritytech/parity/wiki/Proof-of-Authority-Chains)共识机制有许多相似之处。它也可能是针对特定应用链的解决方案，例如[ Cosmos ](https://cosmos.network/)。有关DPoS的其它深入文档，请参阅[此链接](https://bitshares.org/technology/delegated-proof-of-stake-consensus/)以及来自BitShares的[链接](http://docs.bitshares.org/bitshares/dpos.html)以及来自Larimer的[白皮书](https://steemit.com/dpos/@dantheman/dpos-consensus-algorithm-this-missing-white-paper)。

DPoS Features and Tradeoffs 

The core elements of DPoS are the following: 

● Block Producers  

Like other PoS chains, DPoS doesn’t include miners who run hashes to produce blocks . Instead, an elected subset of users is chosen to perform the work of validating the chain. We’ll simply refer to these users are block producers, though they are sometimes called delegates, notaries, validators, forgers, or witnesses.

Because the token holders decide on a elected subset of users to produce blocks, mechanisms to allow a wider group of computers to participate in block production (which ultimately slow down block production) can be removed. DPoS can be seen as a form of “controlled semi-centralization” that gets the benefits of semi-centralization (efficiency and speed) while still maintaining some calculated measure of decentralization (X # of independent block producers that can be voted in and out by token holders). 

DPoSt 特征和利弊

DPoS 的核心元素如下：

-BP（区块生产者）

像其它PoS链一样，DPoS不依靠矿工进行哈希运算来打包区块。相反，其使用一个被选定的部分用户来执行确认链的工作。我们简单地提到这些用户是区块生产者，尽管他们有时被称为委托人，公证人，验证者，伪造者或证人。

因为Token持有者决定一个被选定的部分用户来打包区块，所以可以移除允许更多计算机参与区块打包（可以减缓其出块）的机制。DPoS 可以被看作是一种“可控的弱中心化”形式，它可以获得弱中心化（效率和速度）的好处，同时仍然保持一些适合的去中心化的措施（独立区块生产商的X＃可以通过Token持有人的投票产生）

The multi-billion-dollar question then becomes “How many block producers are necessary in order to be sufficiently decentralized?” This is a loaded question and one that divides the crypto community.
It’s also the single feature that is often presented as a game-ending criticism of DPoS: DPoS is not decentralized enough. 

这个价值数十亿美元的问题就变成了“为了实现足够的去中心化而需要多少区块生产者？”这是一个含混不清的问题，加密社区因此而分道扬镳。

它也有一个类似游戏结束时的点评一样的特征——他们说DPoS不够去中心化。


Importantly, decentralization is a spectrum, and increased decentralization often also incurs higher costs. There are many different measures of decentralization. Some like Balaji Srinivasan have attempted to quantify decentralization, but even he admits that his proposals need more work. He breaks down networks into subsystems, each of which can be measured differently and each of which contributes to an overall notion of system-wide decentralization. Some people may have opposing views about which subsystems to include and how much weight to assign to each. Ultimately, measures of decentralization can produce different results when different variables are examined, and they don’t produce a binary result. Systems are not decentralized or not ; rather, some are more decentralized than others, though this measure can be somewhat subjective. 
重要的是，去中心化是一个范围而已，去中心化的增加往往也会导致更高的成本。有许多不同的去中心化措施。一些类似[Balaji Srinivasan](https://twitter.com/balajis)的人试图[量化去中心化](https://news.earn.com/quantifying-decentralization-e39db233c28e)，但他也承认他的建议需要更多的工作量。他将网络分解成子系统，每个子系统都可以以不同的方式进行测量，每一个都有助于整个系统的去中心化。有些人可能对要包含哪些子系统以及分配给每个子系统的权重有相反的看法。最终，当对不同的变量进行检查时，产生的结果截然不同。无论系统是否去中心化；相反，有些人更愿意去中心化，尽管这种措施可能有点主观。


The goal is not decentralization for its own sake. Decentralization is a feature of systems that
allows them to achieve other goals: censorship resistance, open participation, immunity from
certain attacks, and elimination of single points of failure. While some features that contribute to decentralization can be quantified, the phenomenon as a whole cannot be. The number of block producers is just one metric, but it fails to capture all of the relevant subtleties. It also doesn’t describe how much decentralization is necessary to accomplish the underlying goals, or how to think about theoretical vs practical decentralization。
 
我们的目标不是为了自己的利益而去中心化。去中心化是系统的一个特征，它允许他们实现其它目标：抵制审查，开源参与，免于某些攻击，消除单点故障。虽然有助于去中心化的某些特征可以量化，但整体是不可能。区块生产者的数量只是一个参考标准，它不可能获得所有相关的细节。它也没有描述为实现基本目标需要什么程度的去中心化，或者去中心化在理论与现实上如何实现。

DPoS doesn’t attempt to “find” a balance between the number of block producers needed to ensure that control is sufficiently decentralized and the number of block producers that can easily be monitored for bad behavior. Rather, it explicitly sets the balance, though it can be modified later. 

DPoS并没有试图“找到”一个平衡点，即需要多少区块生产者以确保足够去中心化的控制，以及可以很容易地监控作恶行为的区块生产者的数量。相反，它明确地设置了平衡，尽管它以后可以修改。

There does not seem to be a single number that encapsulates this. In our view, 20 block producers all located in China is less decentralized than 10 block producers spread across various jurisdictions around the globe. Cornell’s IC3 team recently wrote a paper that attempted to quantify decentralization in Bitcoin and Ethereum. They ultimately found that block production in Bitcoin and Ethereum was far more concentrated than commonly thought. They noted: 

我们认为，位于中国的20家地区块生产商的分散程度低于分布在全球各地的10家地块生产商。康奈尔大学的IC3团队最近撰写了一篇论文，试图量化比特币和以太坊的去中心化程度。他们最终发现比特币和以太坊的区块生产比普遍认为的要集中得多。他们指出：


>“These results show that a Byzantine quorum system of size 20 could
achieve better decentralization than proof-of-work mining at a much
lower resource cost. This shows that further research is necessary to
create a permissionless consensus protocol without such a high degree
of centralization.” 

> “这些结果表明，规模为20大小的拜占庭法定人数制度可以实现更好的去中心化，而工作量明显低于资源成本。这表明，对在没有如此高度中心化的情况下创建一个无权限的共识协议进行研究是必要的。


DPoS is one potential solution to this problem; we look forward to more research on this front. The benefits of decentralization can’t be accurately measured by a single number—they are emergent properties that must be observed in an iterative, dynamic, unpredictable, real-world environment.
Token voters in DPoS systems will have to take into account not just how many block
producers there are, but also in which jurisdiction they are located, with whom they are
affiliated, and more. If voters do enough due diligence to ensure that 21 individual entities

located in different jurisdictions are producing blocks, then validation in DPoS has the potential
to be far more decentralized than almost any other blockchain. 

DPoS 是解决这个问题的一个潜在方案；我们期待着在这方面进行更多的研究。去中心化的好处无法用一个单一的数字来准确衡量— 它们是在迭代的，动态的，不可预知的，真实应用环境中表现出的固有特性。

DPoS 系统中的选民不仅需要考虑到有多少个区块生产者，还要考虑他们所处的管辖区域，他们所属的区域等等。如果选民做了足够的调查以确保位于不同司法管辖区的21个独立实体在生产区块，那么DPoS中的验证可能比几乎任何其它区块链分散得多。

For an argument of why DPoS is more decentralized in practice than PoW, see this excellent post from Ian Grigg. In it, he describes how the Chinese government could launch an attack on Bitcoin miners within the country, either by directly taking them over, forcing them to shut down, or exploiting the great fire wall that controls the in/out pipes of the internet in China. This would be hugely disruptive for the Bitcoin network, and would render it severely compromised for a period of time, even if it were eventually able to recover. DPoS, on the other hand, could easily avoid this problem by voting out Chinese block producers and replacing them with block producers in other jurisdictions as soon as (or
even before) the government took action

关于为什么 DPoS 在实践中比 PoW 更去中心化的观点，请参阅[Ian Grigg](https://twitter.com/iang_fc)的[这篇出色的文章](https://steemit.com/eos/@iang/eos-with-dpos-is-immune-to-the-gfw-attack-because-it-is-more-decentralised)。在文章中，他描述了中国政府如何对国内的比特币矿工进行清理政治，要么直接接管，要么迫使他们关闭，要么利用网关控制网络的进出。

这对比特币网络会造成巨大的破坏，并且会在一段时间内严重损害它，即使它最终能够恢复。换句话说，DPoS可以很容易地避免这个问题，只要政府一采取行动（甚至在政府采取行动之前），他们就会投票淘汰中国的区块生产者，以及使用其它司法管辖区的区块生产者代替中国的区块生产者。
One interesting feature of DPoS is that while block producer candidates compete for token holder votes, elected block producers actually cooperate to secure the network during rounds. Block producers share block rewards (from inflation) equally, and they are only allowed to produce one block per round. 
There are no incentives for block producers to compete to try to produce more blocks than the other producers, since this is impossible. In EOS and Steem, block producers are funded entirely by inflation; there are no transaction fees. 

Block producers aren’t incentivized to order transactions based on who pays the highest fee; rather, priority is given relative to overall stake—ownership in the network gives users a claim to bandwidth within the network when the network is at capacity. Block producers compete off-chain to get votes, but once they are voted in they cooperate to secure the chain. And since the number of block producers is fixed, block-producing power doesn’t concentrate,
even with economies of scale.

DPoS 的一个有趣特征是，虽然区块生产者候选人争夺Token持有者的选票，但被选出区块生产者实际上是在以合作的形式保护网络。区块生产者共享区块奖励（来自于增发），他们每轮只允许产生一个区块。不存在区块生产者通过竞争尝试去生产更多区块的动机，因为这是不可能的。在EOS和Steem中，区块生产者完全靠通货膨胀来提供资金；因为没有交易费用。

区块生产者不会因物质利益激励而预定基于谁支付费用高交易；相反，优先考虑的是整体利益——当网络处于最大负荷时，网络中的所有权为用户提供了网络内的带宽要求。

区块生产者了获得选票而竞争，但一旦他们被投票，他们就会合作以确保供应链的安全。而且因为块生产者的数量是固定的，区块生产力不集中，即使是规模经济，也是如此。

