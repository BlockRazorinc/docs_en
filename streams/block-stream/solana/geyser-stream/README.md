# Geyser Stream

## Introduction

**What is Geyser Stream**

Geyser is a plugin mechanism for Solana validators that enables real-time transmission of Solana's account, slot, block, and transaction data to external data storage media. Geyser Stream is a high-performance Solana data streaming service launched by BlockRazor based on the Yellowstone gRPC (Geyser plugin), allowing clients to subscribe to real-time Solana data streams with extremely low latency via the gRPC protocol.



**Applications of Geyser Stream**

Transaction Monitoring: Track transactions for specific accounts, ideal for following smart money trades or targeting new token launches on platforms like pump.fun.

Account Balance Tracking: Monitor balance changes in designated accounts, enabling real-time price calculations for token pairs in DEX pools (e.g., Raydium, Orca, Jupiter).

Block & Slot Insights: Analyze blocks and slots to assess network consensus and health status.



**Key Features of Geyser Stream**

High Performance: Geyser Stream delivers gRPC data streams to clients with ultra-low latency in real time.

Data Integrity: Supports transaction replay for the most recent 500 slots (200 seconds), ensuring seamless data continuity during disconnections.

High Stability: Operates across multiple cloud instances with seamless failover, guaranteeing long-term reliability.



## Endpoint

<table><thead><tr><th width="171.8828125">Region</th><th>Endpoint</th></tr></thead><tbody><tr><td>Frankfurt</td><td>geyserstream-frankfurt.blockrazor.xyz:443</td></tr><tr><td>Amsterdam</td><td>geyserstream-amsterdam.blockrazor.xyz:443</td></tr><tr><td>New York</td><td>geyserstream-newyork.blockrazor.xyz:443</td></tr><tr><td>Tokyo</td><td>geyserstream-tokyo.blockrazor.xyz:443</td></tr></tbody></table>



## How to integrate Geyser Stream

Geyser Stream is available for Tier 2 - Solana and higher-tier users who can refer to the [Authentication](../../../../authentication.md) guide. For multi-language integration details, see:

* [CLI](cli.md)
* [Go](go.md)
* [Rust](rust.md)
* [JS](js.md)



## Periodic Data Allowance

Geyser Stream provides periodic data allowance to users based on subscription plan. Users subscribed to Tier 2 - Solana or higher plans receive free periodic data allowance, with the relationship as follows:

<table><thead><tr><th width="190.875">Tier</th><th>Periodic Data Allowance</th></tr></thead><tbody><tr><td>Tier4 - Solana</td><td>-</td></tr><tr><td>Tier3 - Solana</td><td>-</td></tr><tr><td>Tier2 - Solana</td><td>20 TiB</td></tr><tr><td>Tier1</td><td>50 TiB</td></tr><tr><td>Custom</td><td>Custom</td></tr></tbody></table>

If the free periodic data allowance for the current cycle is exhausted, users can purchase addtional periodic data allowance at the following prices:

<table><thead><tr><th width="210.55859375">Periodic Data Allowance</th><th width="136.5546875">Discount</th><th>Price / Cycle</th></tr></thead><tbody><tr><td>5 TiB</td><td>100%</td><td>$250</td></tr><tr><td>10 TiB</td><td>100%</td><td>$500</td></tr><tr><td>50 TiB</td><td>100%</td><td>$2500</td></tr><tr><td>100 TiB</td><td>95%</td><td>$4750</td></tr><tr><td>150 TiB</td><td>90%</td><td>$6750</td></tr><tr><td>200 TiB</td><td>85%</td><td>$8500</td></tr><tr><td>250 TiB</td><td>80%</td><td>$10000</td></tr></tbody></table>

The steps to purchase periodic data allowance are as follows:

1. Log in to the BlockRazor protal and navigate to Services - Solana - Geyser Stream.
2. Click \[Purchase periodic data allowance], select the periodic data allowance, and click \[Confirm].
3. Choose the service cycle (Note: The start and end times of the cycle align with the subscription plan cycle) and payment method.
4. Complete the payment for the bill.
5. Return to Services - Solana - Geyser Stream to view the periodic data allowance in the overview.

