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

（插入图片）

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
● The appearance of dishonesty, or even a mere lack of sufficient transparency compared
to other candidates
● Greed (e.g. trying to demand higher block rewards than other producers) 
● Censorship
● Malicious collusion 
● Support of controversial or malicious changes to the network 
● Failure to support community-backed changes 
● Regulatory fear based on jurisdiction (for example, Chinese block producers could be
voted out if China announced a crackdown on crypto)

●不诚实行为
●与其他候选人相比，出现不诚实行为，甚至仅仅缺乏足够的透明度
●贪婪（例如试图要求比其他生产者更高的区块奖励）
●审查制度
●恶意串通
●支持对网络进行有争议或恶意的更改
●未能支持社区支持的变更
●基于司法管辖权的监管恐惧（例如，如果中国宣布加强对加密的打击，中国的BP可能会被拒之门外）
