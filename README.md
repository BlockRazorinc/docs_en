---
description: Introduce BlockRazor and the services it provides
---

# About BlockRazor

BlockRazor is a research institution focused on Web3 infrastructure and DeFi trading. It focuses on solving key problems in trading scenarios and continuously transforms its [research results](https://blockrazor.io/blog/) into infrastructure products and services, creating a globally distributed, high-performance multi-chain infrastructure system for builders who pursue excellence.

Through long-term research and engineering practice, BlockRazor provides integrated capabilities covering Transaction Submission, Streams, and Block Builder for Wallets, DEXs, Trading Bots, Searchers, and quantitative trading systems, helping customers obtain faster block transaction signals and better transaction execution results on Ethereum, BSC, Solana, and Base.

### Transaction Submission

BlockRazor offers multiple transaction submission modes to adapt to the different needs of various businesses in terms of mev protection, inclusion speed, and transaction costs:

* [RPC](transaction-submission/rpc/overview.md): Provides standard JSON-RPC methods, offers MEV protection for transactions, and supports real-time rebates.
* [Block Builder](transaction-submission/block-builder/overview.md): A block building service for BSC, providing users with a high-win-rate block building commitment and low-latency access capabilities.
* [Fast](transaction-submission/fast/overview.md): Utilizes [BEF](core-technology/blockchain-edge-fabric.md) to improve inclusion speed, suitable for users with extremely high requirements for transaction speed.
* [Gas Sponsor](transaction-submission/gas-sponsor.md): Provides gas sponsorship for users whose native tokens are insufficient to cover transaction fees, enhancing the user trading experience.

### Streams

BlockRazor offers a variety of high-performance real-time data streaming capabilities, helping trading systems and infrastructure systems obtain signals earlier and synchronize states faster:

* [Mempool](streams/mempool/): Low-latency data streams for mempool pending transactions, enabling real-time monitoring of trading signals in various scenarios such as backrun, copy trading, and sniping.
* [Block Stream](streams/block-stream/): Provides low-latency streams of the latest blocks and confirmed transactions, and is used to monitor confirmation signals, block events, and on-chain results.
* [Node Stream](streams/node-stream/): Helps users synchronize the latest blocks and world state with their own full nodes with lower latency, making it suitable as a low-level input capability for systems that rely on local state.
* [Network Fee Stream](streams/network-fee-stream/): Provides real-time Gas Price, Priority Fee, or Tip data based on recent historical block data, which can be used to optimize transaction parameters and sending strategies.

