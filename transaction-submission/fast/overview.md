---
description: Introduction to Fast Mode of BlockRazor
---

# Overview

### What is Fast mode

Fast is a fast transaction sending mode provided by BlockRazor, aimed at users who have higher requirements for the speed of transaction inclusion, and is applicable to Solana, BSC and Base.

Compared to RPC, Fast focuses more on how to get transactions into the on-chain execution process more quickly after they are sent from the client. It leverages [BEF](../../core-technology/blockchain-edge-fabric.md) to fully utilize the underlying mechanisms of different chains, providing a lower latency sending experience for the trading system.

In Fast mode, sending a transaction requires paying a tip to a designated address within the transaction itself to support a faster transaction processing path. The tip rules, interface formats, and sending methods vary across different blockchains; please refer to the respective blockchain's page for details.

### What users are suitable for Fast mode

* **Wallets / DEXs**: Team aiming to provide a faster sending experience for users worldwide.
* **Trading Bot / Quant Team:** Team with specific requirements for transaction inclusion speed and execution timing

### FAQ

<details>

<summary>What is the difference between Fast and RPC?</summary>

Both Fast and RPC are transaction sending capabilities, but they have different design goals.

RPC focuses more on transaction protection and general access capabilities. It provides standard JSON-RPC methods, focusing on addressing the MEV risks that transactions may encounter during public dissemination, and supports refund and disclosure policy configuration and customized RPC access, making it suitable for Wallets, DEXs, and project teams as a standard transaction sending entry point.

Fast prioritizes the speed of transaction on-chain processing. It optimizes the sending path through [BEF](../../core-technology/blockchain-edge-fabric.md), helping transactions enter the on-chain execution process with lower latency. It is suitable for trading bots, quantitative strategies, and timing-sensitive trading scenarios that have higher requirements for on-chain timeliness.

</details>

<details>

<summary>Why does Fast need tip?</summary>

The core objective of Fast is to help transactions enter the on-chain execution process more quickly, and achieving this typically requires additional sending and execution incentives. Therefore, in Fast mode, transactions need to internally pay a tip to a designated address to support a faster transaction processing path.

From a mechanics perspective, the purpose of a tip is to enable transactions to be processed in Fast mode with a more suitable low-latency execution method. The rules for tips are not entirely the same across different chains; the specific amount, calculation method, and designated address may also differ. Please refer to the specific subpage for details on the corresponding chain.

If you don't want to attach a tip to the transaction, it's better to use standard RPC or other non-Fast sending methods.

</details>
