# Overview

### What are Streams

Streams is a suite of high-performance, real-time data streaming services provided by BlockRazor to deliver low-latency data to trading systems, strategy systems, and infrastructure systems. Unlike Transaction Submission, Streams focuses on "how to see data earlier, how to synchronize state faster, and how to observe the network propagation process in more detail.

For Searcher, Trading Bot, Wallet, DEX, and quantitative trading systems, signal acquisition speed, state synchronization speed, and cross-region data consistency directly impact strategy effectiveness and execution quality. Streams' core value lies in helping users acquire critical on-chain data with lower latency, primarily addressing four types of issues:

* Detect unconfirmed transactions and order flow signals earlier
* Get the latest blocks and confirmed transactions faster
* Get timely references for Gas Price, Priority Fee, or Tip.
* Synchronize local nodes with the latest world state with lower latency

### What capabilities does Streams provide

#### Mempool

Mempool is used to obtain unconfirmed transaction or private order stream data with low latency, making it suitable for scenarios that require capturing on-chain signals as early as possible.

* [**Public Mempool**](mempool/bsc/public-mempool.md)**:** Used for low-latency subscription to pending transactions, suitable for monitoring public trading signals.
* [**Private Mempool**](mempool/bsc/private-mempool.md)**:** Used for subscribing to private orderflow, suitable for scenarios such as backrun.
* [**Tx Trace**](mempool/bsc/tx-trace.md)**:** Used to observe the propagation path and cross-regional latency distribution of transactions in the Public Mempool, suitable for transaction latency investigation, multi-regional deployment evaluation, and propagation effect verification.

#### Block Stream

Block Stream is used for low-latency retrieval of the latest blocks and confirmed transactions, making it suitable for scenarios that focus on post-confirmation signals, block events, and on-chain results. Compared to Mempool, Block Stream observes "data that has already entered the block," while Mempool focuses more on "data that has not yet been confirmed but has entered the propagation process." For systems that need to confirm transaction results, track block events, or perform block-level analysis, Block Stream is more suitable.

#### Network Fee Stream

Network Fee Stream is used to obtain real-time fee references such as Gas Price, Priority Fee, or Tip based on recent historical block data. This type of data is suitable for:

* Dynamically adjust trading parameters
* Optimize fee strategy
* Assisted transaction sending decision

#### Node Stream

[Node Stream](node-stream/) is used for low-latency synchronization of the latest blocks and world state, and is suitable for systems that rely on local node state for decision-making.

Unlike subscribing to Block Stream, Node Stream doesn't simply push block data; instead, it allows users' own full nodes to synchronize faster via [BEF](../core-technology/blockchain-edge-fabric.md). For teams that need to obtain the latest status immediately and directly rely on local nodes to run strategies or services, Node Stream is more suitable as an underlying infrastructure capability.

### How to choose a suitable Stream

| 場景                                                                  | 適用用戶                                            | 推薦能力               |
| ------------------------------------------------------------------- | ----------------------------------------------- | ------------------ |
| monitor pending transactions and backrun / copy trading / sniping   | Searcher, Trading Bot                           | Public Mempool     |
| subscribe provite orderflow and backrun / copy trading / sniping    | Searcher, Trading Bot                           | Private Mempool    |
| Dynamic optimization for Gas / Priority Fee / Tip                   | Searcher, Trading Bot, Quant Team, Wallets, DEX | Network Fee Stream |
| Keep local nodes and world state up-to-date                         | Searcher, Trading Bot, Quant Team, Wallets, DEX | Node Stream        |
| Observe the transaction propagation path and cross-regional latency | Searcher, Trading Bot, Quant Team               | Tx Trace           |
| Subscribe Base FlashBlock Stream                                    | Searcher, Trading Bot, Quant Team, Wallets, DEX | FlashBlock Stream  |
| Subscribe Solana accounts、transactions、slots and blocks             | Searcher, Trading Bot, Quant Team, Wallets, DEX | Geyser Stream      |
| Obtain shreds from Solana with extremely low latency.               | Searcher, Trading Bot                           | Shred Stream       |

### Quick Start

{% stepper %}
{% step %}
**Purchase Stream**

Go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase the target stream.
{% endstep %}

{% step %}
**Apply for auth**

For details, see [Authentication](../get-started/authentication.md)
{% endstep %}

{% step %}
**Integrate Stream**

Based on the target stream access documentation, access the target stream and test its latency and stability performance.
{% endstep %}
{% endstepper %}

### FAQ

<details>

<summary>What is the difference between Public Mempool and Private Mempool?</summary>

Public Mempool is used to subscribe to publicly disseminated pending transactions, making it suitable for early detection of trading signals.\
Private Mempool is used to subscribe to private pending transactions, and is suitable for scenarios such as backrun.

</details>

<details>

<summary>What are the differences between Mempool and Block Stream?</summary>

Mempool focuses on transactions that are not yet confirmed but have entered the propagation process; Block Stream focuses on blocks and transactions that have entered the block and have been confirmed.

If you want to discover opportunities earlier, prioritize Mempool; if you are more concerned with result confirmation and block-level analysis, prioritize Block Stream.

</details>

<details>

<summary>What is the difference between Block Stream and Node Stream?</summary>

Block Stream is a subscription-based data stream used to obtain the latest blocks and confirmed transactions with low latency.

Node Stream, on the other hand, focuses more on infrastructure capabilities, allowing users' own full nodes to synchronize the latest blocks and world state faster.

If you only need block data, Block Stream is usually more straightforward; if you need to run the system based on the state of local nodes, Node Stream is more suitable.

</details>

