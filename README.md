# About BlockRazor

### Introduction

BlockRazor is a leading Web3 transaction infrastructure provider. Leveraging top-tier distributed network communication technology and architecture, BlockRazor serves a diverse range of users, including wallets, DEXs, trading bots, searchers, and quantitative trading systems. BlockRazor has launched core services such as Transaction Submission, Streams, and Block Builder across mainstream public chains including Ethereum, BSC, Solana, and Base, helping clients achieve optimal trade execution.

### Transaction Submission

BlockRazor offers multiple transaction submission modes—including RPC, Gas Sponsor, Fast, and Bundle—tailored to specific client requirements:

* RPC: Provides standard JSON-RPC methods with integrated MEV protection and support for real-time rebates.
* Gas Sponsor: Provides Gas sponsorship for users who lack sufficient native tokens to pay transaction fees, significantly enhancing the user onboarding and trading experience.
* Fast: Utilizes a global acceleration network to boost on-chain transaction speeds, ideal for users with extreme latency requirements.
* Bundle: Enables users to execute transactions within the same block with the "signal transaction" via Bundles, specifically designed for scenarios like backrunning, copy trading, and token sniping.

### Streams

BlockRazor provides a variety of high-performance data streams, including Mempool, Block Stream, Network Fee Stream, and Node Stream:

* Mempool: Delivers low-latency pushes of pending transactions, allowing users to monitor signal transactions for backrunning, copy trading, and sniping in real-time.
* Block Stream: Provides low-latency block data for trading program to monitor confirmed signal transactions or other transactions as they happen.
* Network Fee Stream: Real-time pushes of Gas Price, Priority Fee, or Tips based on recent historical block data.
* Node Stream: Synchronize data with full nodes for low latency and keep the world state updated in real-time.

### Block Builder

[Block Builder](block-builder/block-builder/) provides BSC block building services based on PBS architecture. Deployed in multiple regions around the world with low-latency communication to validators, Block Builder run multiple algorithms to maximize the block value, realizing the construction of competitive blocks. BlockRazor's Block Builder has a historical cumulative block production rate of 37%, ranking first in the entire BSC chain. To view the real-time block production rate, please visit [https://dune.com/bnbchain/bnb-smart-chain-mev-stats](https://dune.com/bnbchain/bnb-smart-chain-mev-stats).

