● Centralization of block production?
- 中心化的区块生产


The most notable feature of any DPoS-powered protocol is that the number of block producers is explicitly limited. The number of block producers varies in different implementations—101 in Lisk, 21 in EOS, etc. Often the number itself is a parameter that can be changed by a token holder vote.?

任何DPoS共识的最显着的特点是出块人的数量是明确限制的。区块生产者的数量在不同的应用中有所不同—— 在 Lisk 中有 101 个，在 EOS 中有 21 个等等。就这个数字本身来说，是可以通过 Token 持有者投票来改变的一个参数。


DPoS validation happens in rounds; each round consists of a period in which each block producer is given one slot to produce a block. In Lisk, for example, a round would consist of 101 blocks. At the beginning of each round, each block producer is assigned a slot. Each slot corresponds to one block and is the only time in that round in which the assigned block producer can produce a block.
 If a producer fails to create a block during their slot, then that block is skipped and the transactions from that slot are included in the next block. Token holder votes are tallied each round, and block producers can be voted in or out each round. In every DPoS implementation, the number of potential block producers is always greater than the number of producers allowed in each round. Thus, there are always block producers ready to step in if a malicious producer is voted out. It is also possible to configure DPoS parameters to compensate backup block producers in order to incentivize them to be ready to fill the spots of producers that are voted out (see ?total witnesses? in Steem).?

 DPoS 需要在每轮投票中进行验证；而每轮都需要一定时间段，每个区块生产者在这个时间段内产生一个区块。例如，在 Lisk 中，一个回合将由 101 个块组成。在每轮开始时，每个区块生产者都被指定一个时间段。每个时间段对应一个区块，并且是该轮中唯一分配的区块生产者可以生成区块。如果出块人在该时间段内未能打包一个块，那么该块将被跳过，并且来自该时间段的交易将被打包在下一个区块中。 Token 持有者的投票每轮统计一次，而区块生产者在每轮投票中要么被选中要么出局。在每个 DPoS 应用中，备份的出块人数量总是大于每轮需要的数量。因此，如果出块人作恶，那么将会被投票出局，备份的区块生产者将会及时介入。同时，也可以配置 DPoS 参数来补偿备份区块生产者，以激励他们随时准备好补充被投票出局者的位置（参见[Steem中的所有见证人](https://steemd.com/witnesses)）。


Collusion and censorship by validators is always a concern with any blockchain protocol. If three of the largest Ethereum mining pools colluded, it would be possible for them to pierce the safety of the
network. 
DPoS is aware of these risks and attempts to mitigate them through transparency. In DPoS, token holders are directly responsible for deciding who controls validation. While this puts more responsibility on individual token holders, it also means that the owners of the network have recourse if validators behave badly.  If Ethereum mining pools colluded, individual miners participating in the pool would have to point their miners elsewhere, or the community would have to hard fork the network.  Both scenarios require some form of off-chain coordination. If DPoS block producers colluded, the community could vote them out within a single round and replace them with honest block producers. This still requires a form of ex-protocol coordination (token holders deciding how to re-allocate their votes), but it is more formalized and arguably more trivial to enact. This architecture allows DPoS to introduce a form of centralization while still maintaining security. The implications of this (as well as potential attack vectors) will be explored later in this document.?

任何区块链协议都始终关注验证者的作恶和审查。如果三个最大的[以太坊采矿池](https://etherscan.io/stat/miner?range=7&blocktype=blocks)相互勾结，这将有可能颠覆网络的安全。

DPoS 意识到这些风险，并试图通过透明度来减轻风险。在 DPoS 中，Token 持有者直接负责决定谁控制验证。虽然这样一来，Token 持有者需要承担更多责任，但这也意味着，如果验证人作恶，网络所有者就可以求助。但如果以太坊矿池相互勾结串通，那么参与矿池的个体矿工将不得不跟随矿主，否则社区将不得不艰难地进行分叉。
这两种情况都需要某种形式的离线协调。如果 DPoS 区块生产者作恶，社区可以在单轮投票中将它们投票出去，并将其替换为诚实可靠的区块生产者。这仍然需要一种预先共识协议的形式（ Token 持有者决定如何重新分配他们的选票），但它更形式化，并且可以说更加微不足道。这种架构允许 DPoS 在保持安全性的同时采用一种中心化的形式。这个（以及潜在的攻击载体）含义将在本文稍后部分讨论。

- Scalability 

- 可扩展性

Known and limited block producers means that blocks can be propagated through the network much
more efficiently, enabling significant scalability increases. Blocks can also be consistently and reliably
produced in a much smaller time frame (BitShares currently produces a block every 3 seconds).

已知和有限的区块生产者意味着区块可以更有效地通过网络传播，从而显着提高可扩展性。区块也可以在更小的时间范围内持续可靠地生成（比特股目前每3秒产生一个块）。

Furthermore, finality can be reached as soon as ⅔ of the block producers have confirmed a
transaction, with strong guarantees that a transaction is on a valid chain even before that. 

此外，只要有 2/3 的区块生产者确认交易，就可以强有力的保证，即使在此之前，交易也在有效的链条上。

While DPoS is certainly more scalable than PoW, exactly how fast it can go depends on a variety of
factors. EOS is attempting to optimize for extremely high throughput by using the WASM virtual
machine and employing a message-based architecture instead of a state-based one. Early results
showed 50,000 tps on an EOS smart contract, but those results are not indicative of full-scale main net performance. Recently, the community-run EOS test net hit 600 tps with beta software and
non-specialized machines, and Larimer recently claimed in an update that the software could be set to
debut with 5,000 tps in its single-threaded architecture before moving to parallel execution. 

虽然 DPoS 肯定比 PoW 更具扩展能力，但它的运行速度取决于一系列因素。 EOS 试图通过使用 WASM 虚拟机并采用基于 message 的体系结构而不是基于 state 的体系结构来优化达到极高的吞吐量。早期的结果显示 EOS 智能合约为 50,000 tps ，但这些结果并不代表全面的网络性能。最近，社区利用beta软件和非专业化的机器，运行 EOS 测试网的结果达到 600 tps ，而 Larimer 最近在一次更新中声称，在转向并行执行之前，该软件在其单线程架构中首次就达到 5,000 tps 。


It is worth noting that three of the top 5 blockchains with the most operations performed daily are
DPoS blockchains, according to Blocktivity.info. And while Ethereum is consistently operating at near
capacity, both BitShares and Steem have no pending transactions and plenty of bandwidth to spare.
Smart contract platforms that host large-scale dApps need to be able to handle many thousands of
operations per second, whether they are simple likes or million-dollar value transfers. This chart
provides a great breakdown of operation type and count for BitShares, while this link provides
statistics for Steem. For more information on how BitShares achieves its performance, see detailed
explanations here and here. 


根据[Blocktivity.info](https://www.blocktivity.info/)的数据，值得注意的是，每天执行的操作最多的前 5 个区块链中有 3 个是 DPoS 区块链。尽管以太坊一直以接近100%满负荷运转（译者注：还有大量未处理的交易），但BitShares和Steem都不存在未完成的交易，同时又大量的可用带宽。大型dApp的智能合约平台需要每秒处理数千次操作，无论它们是单纯的赞还是百万美元的价值转移。[此图表](http://www.cryptofresh.com/charts)提供了BitShares的操作类型和计数的详细分类，而[此链](https://steemdb.com/)接提供了Steem的统计信息。有关BitShares如何实现其性能的更多信息，请参阅[此处1](https://bitshares.org/technology/industrial-performance-and-scalability/)和[此处2](https://bitshares.org/blog/2015/06/08/measuring-performance/)的详细说明。

- Network Infrastructure as a Service 

- 网络基础设施服务


Every blockchain network can be divided into two major subsets of actors—those who perform
operations on the network and those who validate the operations. We can refer to the first group as
users and the second group as validators. 

每个区块链网络可以分为两个主要的角色子集——即在网络上执行操作的人员和验证操作的人员。我们可以将第一组称为用户，将第二组称为验证者。

In Bitcoin, Ethereum, Monero and other proof of work-based blockchains, the validators are miners.
Miners race to solve computationally intensive puzzles, and the first to solve the puzzle is allowed to
produce a block (and collect transaction fees and the block reward). In traditional PoS, users must
bond their tokens, and they are awarded the ability to produce blocks proportional to their bonded
stake. 

在比特币，以太坊， Monero 和其它基于工作量证明（ PoW ）的区块链中，验证者都是矿工。矿工们竞相去解决一道高难度谜题，第一个解出谜题的被允许打包一个区块（获取交易费用和区块奖励）。在传统的 PoS 中，用户必须锁定他们的 Token ，才可以获取与其锁定的 Toekn 成比例的生产区块的能力


In each of these scenarios, validators are providing key network infrastructure: They are collecting
transactions, ordering them, and preventing double-spends. In PoW, validators are those with access
to the best hardware and cheapest electricity. In PoS, validators are those with large ownership stakes
in the network. In DPoS, however, the validators can be thought of as contractors that are hired by the
owners of the network (token holders). They are hired (voted in), given a job (to produce blocks), paid
(through inflation or transaction fees), and can be fired (voted out) for not performing their duties. 

在每种情况下，验证者都在提供关键的网络基础设施：他们正在罗列交易，排序，并防止双重支付。在 PoW 中，验证者是那些可以使用最好的硬件和最便宜的电力的机器。在 PoS 中，验证者是那些在网络中拥有大量权益（ stake ）的人。但是，在 DPoS 中，验证者可以被认为是由网络所有者（Token持有者）雇用的承包商。他们被雇佣（投票产生），得到一份工作（生产区块），被支付（通过通货膨胀或交易费用），并且可能因不履行职责而被解雇（被投票出局）。


This structure means that DPoS network token holders, as the owners of the network, ultimately have
control over who provides infrastructure, while Bitcoin and Ethereum give token holders no choice. If
miners misbehave, as they have incentive to do, users have no recourse. DPoS is the only algorithm
that allows infrastructure providers to be easily fired  (no slashing required) and replaced for not
providing a good service. Reasons for firing could include any of the following: 


这种设计意味着DPoS的网络Token持有者，即网络的所有者，基本上能够控制谁提供基础设施，而比特币和以太坊的Token持有人别无选择。如果矿工行为不当，即他们有作恶动机的话，用户就无法求助。而DPoS是另一种规则系统，即允许基础设施提供者（即节点）易于被解雇（不需要大幅削减），并由提供良好服务的节点所代替。解雇的理由可能包括以下任何一种情况：


● Dishonesty 

● The appearance of dishonesty, or even a mere lack of sufficient transparency compared to other candidates

● Greed (e.g. trying to demand higher block rewards than other producers) 

● Censorship

● Malicious collusion 

● Support of controversial or malicious changes to the network 

● Failure to support community-backed changes 

● Regulatory fear based on jurisdiction (for example, Chinese block producers could be voted out if China announced a crackdown on crypto)

●不诚实行为

●与其他候选人相比，出现不诚实行为，甚至仅仅缺乏足够的透明度

●贪婪（例如试图要求比其他生产者更高的区块奖励）

●审查制度

●恶意串通

●支持对网络进行有争议或恶意的更改

●未能支持社区支持的变更

●基于司法管辖权的监管恐惧（例如，如果中国宣布加强对加密的打击，中国的BP可能会被拒之门外）

● On-Chain Governance
链上治理


DPoS is inherently a form of on-chain governance; it uses stake-weighted voting to allow the owners
of the network (token holders) to make decisions about the network. DPoS is a form of liquid
representative democracy where voting power can be allocated to other participants and votes can be
changed at any time. While voting for block producers is the primary governance use case, token
holder voting can also be used to decide on things like development funding, monetary policy,
network parameters, hard forks and more.?

DPoS 本质上是一种链上治理形式；它采用权益权重投票形式允许网络的所有者（Token持有者）对网络做出决定。DPoS是一种流动的代议制民主形式（译者注：DPoS：超级节点是变化的，因为持币者可以投票选择或淘汰他们，另外他们代表普通持币者的利益），即可以将投票权分配给其他参与者，并且可以随时更改投票权。虽然对区块生产者投票是主要的治理应用，但Token持有人得投票也可用于对发展基金，货币政策，网络参数，硬分叉等等做出决定。

Blockchain governance is still very much a nascent field, and there exists a lot of disagreement over
which approach to blockchain governance is the most promising. Some, like Ethereum researcher
Vlad Zamfir?, ?have argued? that on-chain governance is a bad idea because, among other reasons, it
negates the role of non-block-producing full nodes in the governance process. Analyst ?Nic Carter
similarly concluded? that Bitcoin’s informal off-chain governance, which consists of several different
social and technological layers, is the ideal form of governance for a decentralized network. Fred
Ehrsam, co-founder of Coinbase, ?argued for? on-chain governance as a way to bring formal structure
to these messy interactions. Many point to the ?Bitcoin scaling debate?, the ?Ethereum DAO fork?, and the
recent ?Parity wallet bug? debate as three examples of situations where on-chain governance could
have more easily rectified very messy and uncertain situations.?

区块链治理仍然是一个新兴领域，关于区块链治理最有前途的方案上存在很多争议。有些人，例如以太坊研究员 [Vlad Zamfir](https://twitter.com/VladZamfir) ，[认为](https://medium.com/@Vlad_Zamfir/against-on-chain-governance-a4ceacd040ca)链上治理是一个糟糕的主意，因为除了其它原因之外，它否定了在治理过程中无区块生成（ non-block-producing ）全节点的作用。

分析师 [Nic Carter](https://twitter.com/nic__carter)得出类似的[结论](https://coinmetrics.io/papers/dissertation.pdf)：比特币非正式的链下治理由几个不同的社会（确定一下最终意思）和技术层组成，是去中心化网络的理想治理形式。
Coinbase的联合创始人Fred Ehrsam[认为](https://medium.com/@FEhrsam/blockchain-governance-programming-our-future-c3bfe30f2d74)，链上治理是将正式结构带入这些混乱交互的一种方式。

许多人指出[比特币扩之争](https://hackernoon.com/the-great-bitcoin-scaling-debate-a-timeline-6108081dbada)，[以太坊 DAO 分叉](https://www.cryptocompare.com/coins/guides/the-dao-the-hack-the-soft-fork-and-the-hard-fork/)以及最近的 [Parity 钱包 bug](https://paritytech.io/a-postmortem-on-the-parity-multi-sig-library-self-destruct/) 争论的三个例子，进一步说明了链上治理可以更容易地纠正非常混乱和不确定的情况。





DPoS chains embrace the fact that all blockchain networks are inherently political and seek to
formalize the political process. While there are certainly issues with on-chain governance and token voting (which we’ll explore later), both are key features of DPoS. DPoS is a community-owned
operational hierarchy that operates in a fully transparent, decentralized way. While it is not clear that
on-chain governance is better than other forms of blockchain governance, it certainly isn’t clear that it
is worse. We believe strongly that this approach should be tried and tested.?


DPoS链表明，所有区块链网络本质上都是政治性的，并寻求形式化政治过程。尽管链上治理和Token投票肯定存在问题（我们将在后面讨论），但两者都是DPoS的关键特征。DPoS是一个拥有操作性层级的社区，以完全透明的，去中心化的方式运作。虽然链上治理不如其它形式的区块链治理更好，但不一定是最糟糕的方式。因此我们强烈建议应该尝试和测试这种方法。

● Self-Funding Through Inflation?
通过通货膨胀筹集资金


Almost every major blockchain pays for infrastructure with inflation. In the case of Bitcoin and
Ethereum, miners receive block rewards as compensation for validating the blockchain. When block
rewards run out in the future, infrastructure will have to be supported through fees alone. This raises
questions about how high fees will get in the future, how that will affect incentives to mine, and
whether that will affect the security of the chain.?

几乎每一个主要的区块链都是通过通货膨胀来应对基础设施建设。对比特币和以太坊来说，矿工获得区块奖励作为打包区块链的报酬。那么如果区块奖励在未来某个时间点用完了怎么办，基础设施则必须通过收费来获得支撑。这使得收多高费用成了一个问题，因为这会影响到激励的效果和链的安全性。


EOS and Steem, because they have no transaction fees, use an entirely different model. Not only do
they use inflation to pay block producers to provide infrastructure, but they also use inflation to fund
the development of the platform itself. Token holders can vote on a maximum annual inflation rate,
initially set at 5%. This number can be changed, as it has been several times ?in Steem?. Token holders
also vote on how much of the annual inflation is paid directly to block producers. If the token price
increases, users can decide whether to keep block producer pay steady (by lowering block rewards)
or to allow block producers to capture additional profits that can be used to scale up their
infrastructure. That which is not paid to block producers can be paid to a set of community smart
contracts that can be used in a wide variety of ways. A contract could be a development fund that
pays out developers based on community votes; it could go directly to a company that is actively
working on development; it could be used to fund hackathons; it could be burned; and more. DPoS
actually makes it possible for developers, marketers, and others building community tools to be
funded ?by the blockchain itself

EOS和Steem，它们没有交易费用，且使用完全不同的模型。即它们不仅通过通货膨胀来支付区块生产者提供基础设施的费用，而且还通过通货膨胀来资助平台本身的开发。

Token持有者可以对年度通货膨胀率进行投票，最初定为5％。这个数字时可以改变的，因为它在[Steem](https://github.com/steemit/steem/issues/551)中已经尝试过了。Token持有者还会投票决定每年的通货膨胀有多少是直接用来支付给BP。如果Token价格上涨，用户可以决定是否要给予区块生产者固定的支付（通过降低区块奖励）或允许区块生产者获取可用于扩大其基础设施的额外利润。那些没有支付给区块生产者的费用（Token）可以支付给一些以各种方式使用的社区智能合约。某个合同可以是一个开发基金，它根据社区投票给开发者支付费用；也可以直接投给一个积极致力于发展的公司；也可以用来资助黑客马拉松：它也可以被销毁等等。DPoS实际上可以让开发人员，营销人员和其他构建社区工具的人*通过区块链本身*获得资金支持。


Many people struggle with the concept of inflation and are adverse to relying on inflation funding. This
shouldn’t be the case. Inflation is perhaps the only method by which blockchains can be funded in a
fair way because it solves the tragedy of the commons problem. Some blockchains, like Monero, rely
entirely on community crowdfunding of development initiatives. While the generosity of the Monero
community is remarkable, it remains unclear whether that is a sustainable way to fund development.
Everyone benefits from the development advances made, but only a minority of users are willing to
contribute their own money to funding. With inflation funding, all users collectively fund development
and security ratably, and they all collectively reap the benefits. As Fred Ehrsam points out, inflation
funding can actually be a net positive for token holders: 

许多人纠结于通货膨胀的概念上，但这一切对依赖通货膨胀的资金是不利的。不应该是这样的。通货膨胀或许是区块链能够以公平的方式获得资金的唯一方法，因为它解决了公地悲剧。

像 Monero 这样的一些区块链，完全依靠社区众筹的发展举措。虽然 Monero 的社区很大方，但这是否是一种可持续的发展方式尚不清楚。每个人都能从项目的发展中获益，但只有少数用户愿意出钱。但如果通过通货膨胀获取资金，那么相当于所有的用户*共同*为项目的发展和安全提供资金。正如 Fred Ehrsam 所[指出的那样](https://medium.com/@FEhrsam/funding-the-evolution-of-blockchains-87d160988481)，通货膨胀提供的资金实际上可以为 Token 持有者带来净收益（ a net positive ）：

> “If Ether holders believed an upgrade (ex: sharding) would make the price go up by >10%, they’d be happy to pay close to 10% of their tokens for it. That means Ethereum could crowd fund a $3bn feature boun ty by inflating the number of ETH by 10% and pay the newly created tokens to the creator(s) of the upgrade.This is somewhat analogous to taxes: everyone in the community chips in to fund common infrastructure (ex: roads) which no one would build alone.”

> 如果以太坊持有者认为升级（例如：分片）会使价格上涨 > 10％，他们会很乐意为其支付接近 10％ 的 Token 。这意味着以太坊可以通过通货膨胀增发  10％ ETH 来筹集30亿美元，  并将增发的 Token 支付给系统升级的创建者们。这有点类似于税收：社区中的每个人都在为共同的基础设施（例如：道路）提供资金，而这不是哪一个可以单独完成的。



Every blockchain must pay to secure its network through either transaction fees, inflation, or both.
Transaction fees force active users to pay, while passive users (hodlers) don’t. A user could secure her
entire life savings in Bitcoin or Monero without almost ever contributing to the security of the platform
through transaction fees. This creates a free-rider problem. Transaction fees are also variable and
unpredictable, and may need to be astronomically high in order to pay for network security. Inflation is
a more  equitable and user-friendly way of securing the network.?

每个区块链都必须通过交易费用，通胀或二者并存的方式来保证其网络安全。交易费由活跃用户支付，而 Token 持有者（ hodlers ）不支付。用户可以通过比特币或 Monero 储存其一生的积蓄，而不需要为平台的安全性承担任何费用。这产生了一个搭便车问题。交易费用是变动的也是不可预测的，因此为了网络安全，交易费用可能是一个天文数字。基于以上分析看来，通货膨胀是一种更加公平和人性化的保护网络的方式。

Similar approaches have been tried by other projects in a number of ways. Zcash collects a
“?Founders’ Reward?,” that sends 10% of the total money supply to the Zcash Company and its
shareholders. Dash collects a portion of block rewards for a masternode-vote development fund.
DPoS formalizes these arrangements, bakes them directly into the protocol, and allows for maximum
flexibility and accountability.?

已经有不少项目以多种方式尝试了类似的方法。Zcash 采用了[“创始人奖励”](https://blog.z.cash/funding/)（即利益相关者），它将总 Token 供应量的 10％ 奖励给 Zcash 公司及其投资者。 Dash 回收了区块奖励的一部分用于主节点的[开发基金](https://dashvotetracker.com/)。而 DPoS 将这些动作全部正式化，即将其直接放到协议中，并给予了最大限度的灵活性和问责性（ flexibility and accountability ）。
