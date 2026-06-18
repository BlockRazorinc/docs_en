---
description: Introduces the pricing of BlockRazor products and services
---

# Pricing

{% hint style="info" %}
BlockRazor's pricing system has been fully upgraded, separating the functionalities of the original multi-chain, multi-tier system into independent services. These services support individual subscriptions or bundled purchases with other services, lowering the subscription threshold while precisely matching user needs. See [Subscription Services](pricing.md#subscription-service) for details. Furthermore, new registered users can still enjoy multi-mode transaction sending services on Solana, BSC, Ethereum, and Base with zero barriers to entry. See [New Registered Users](pricing.md#new-registered-users) for details.
{% endhint %}

### Subscription service

#### Personalized

{% hint style="info" %}
Users can freely combine and purchase services across chains. Stream-type services support configuring quantities or traffic package specifications, and also support daily purchases; see [Pricing](https://blockrazor.io/#/pricing) page for details.
{% endhint %}

{% tabs %}
{% tab title="BSC" %}
<table><thead><tr><th width="194.09765625">Service</th><th>Description</th><th>Price</th></tr></thead><tbody><tr><td><a href="../transaction-submission/fast/bsc/broadcast-tx.md">Broadcast Tx</a></td><td>Propagating transactions and transaction batches with low latency</td><td>$500 / month</td></tr><tr><td><a href="../streams/mempool/bsc/public-mempool.md">Public Mempool</a></td><td>Subscribe to mempool transactions with low latency</td><td>$300 / stream / month</td></tr><tr><td><a href="../streams/mempool/bsc/private-mempool.md">Private Mempool</a></td><td>Subscribe to BlockRazor RPC orderflow</td><td>$1000 / month</td></tr><tr><td><a href="../streams/block-stream/bsc/newblocks.md">Block Stream</a></td><td>Subscribe to blocks with low latency</td><td>$500 / stream / month</td></tr><tr><td><a href="../streams/node-stream/bsc/full-node-synchronization.md">Node Stream</a></td><td>Low-latency synchronized world state</td><td>$800 / enode / month</td></tr><tr><td><a href="../streams/network-fee-stream/bsc/getgaspricestream.md">Network Fee Stream</a></td><td>Obtain BSC gas price data</td><td>$500 / month</td></tr><tr><td><a href="../transaction-submission/block-builder/trace-bundle.md">Bundle Tracing &#x26; Explorer</a></td><td>Tracing and explore bundle of Block Builder</td><td>$1500 / month</td></tr></tbody></table>
{% endtab %}

{% tab title="Solana" %}
<table><thead><tr><th width="175.34765625">Service</th><th>Description</th><th>Price</th></tr></thead><tbody><tr><td><a href="../streams/block-stream/solana/shred-stream.md">Shred Stream</a></td><td>Low-latency transmission of shreds</td><td>$500 / stream / month</td></tr><tr><td><a href="../streams/block-stream/solana/geyser-stream/">Geyser Stream</a></td><td>Real-time transmission of on-chain data from Solana, including accounts, slots, blocks, and transactions.</td><td>5 TiB - $250 / month<br>10 TiB - $500 / month<br>50 TiB - $250 / month<br>100 TiB - $4750 / month<br>150 TiB - $6750 / month<br>200 TiB - $8500 / month<br>250 TiB - $10000 / month</td></tr><tr><td><a href="../streams/network-fee-stream/solana/get-transactionfee.md">Network Fee Stream</a></td><td>Get Solana priority fee and tip data</td><td>$300 / month</td></tr></tbody></table>
{% endtab %}

{% tab title="Base" %}
<table><thead><tr><th width="145.37890625">Service</th><th>Description</th><th>Price</th></tr></thead><tbody><tr><td><a href="../streams/block-stream/base/get-flashblockstream/">FlashBlock Stream</a></td><td>Low-latency acquisition of Base FlashBlock data</td><td>$250 / stream / month</td></tr><tr><td><a href="../streams/block-stream/base/get-blockstream.md">Block Stream</a></td><td>Low-latency acquisition of Base Block data</td><td>$300 / stream / month</td></tr><tr><td><a href="../transaction-submission/rpc/base/eth_sendrawtransaction.md">RPC-Send Tx</a></td><td>Low latency and high TPS for sending base transactions on-chain</td><td>$1000 / month</td></tr></tbody></table>
{% endtab %}

{% tab title="General" %}
| Service           | Description                 | Price     |
| ----------------- | --------------------------- | --------- |
| Dedicated Channel | Dedicated technical support | $1000 / 月 |
{% endtab %}
{% endtabs %}

#### Package

{% hint style="info" %}
Compared to purchasing individual services, users can complete a package purchase at a lower price through the Package. Currently, the Package mainly includes the BSC service, with a total subscription price of **$1250/month**. Specific services are as follows:
{% endhint %}

<table><thead><tr><th width="177.390625">服務</th><th>描述</th></tr></thead><tbody><tr><td><a href="../streams/mempool/bsc/public-mempool.md">Public Mempool</a></td><td>Subscribe to high-performance network transaction data</td></tr><tr><td><a href="../streams/block-stream/bsc/newblocks.md">Block Stream</a></td><td>Subscribe to high-performance network block data</td></tr><tr><td><a href="../streams/node-stream/bsc/full-node-synchronization.md">Node Stream</a></td><td>Low-latency synchronized world state</td></tr><tr><td><a href="../transaction-submission/block-builder/call-bundle.md">Call Bundle</a></td><td>Submit a request to Block Builder to receive bundle simulation results</td></tr><tr><td><a href="../transaction-submission/block-builder/fast-submit.md">Fast Submit</a></td><td>Submit transactions to Block Builder with lower latency and higher stability</td></tr><tr><td><a href="../streams/mempool/bsc/tx-trace.md">Tx Trace</a></td><td>Monitoring transaction propagation paths and cross-regional latency distribution</td></tr></tbody></table>

#### Discount&#x20;

The relationship between discounts and subscription periods is as follows:

<table><thead><tr><th width="314.41796875">Periods</th><th width="328.90234375">Discount</th></tr></thead><tbody><tr><td>1 month</td><td>-</td></tr><tr><td>3 months</td><td>5% off</td></tr><tr><td>6 months</td><td>10% off </td></tr><tr><td>9 months</td><td>15% off</td></tr><tr><td>12 months</td><td>20% off</td></tr></tbody></table>

### New registered users

{% hint style="info" %}
BlockRazor offers new registered users multi-mode transaction sending services on Solana, BSC, Etherem, and Base, including RPC, Fast, Bundle, and Block Builder modes.
{% endhint %}

#### RPC

<table><thead><tr><th width="125.16015625">Chain</th><th>Methods</th><th>Limit</th></tr></thead><tbody><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/rpc/bsc/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li><li><a href="../transaction-submission/rpc/bsc/eth_sendmevbundle/"><code>eth_sendMevBundle</code></a></li><li>Other JSON RPC methods</li></ul></td><td>-</td></tr><tr><td>Ethereum</td><td><ul><li><a href="../transaction-submission/rpc/ethereum/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li><li><a href="../transaction-submission/rpc/ethereum/eth_sendbundle.md"><code>eth_sendBundle</code></a></li><li>Other JSON RPC methods</li></ul></td><td>-</td></tr><tr><td>Base</td><td><ul><li><a href="../transaction-submission/rpc/base/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li></ul></td><td>1 Tx / 5s</td></tr></tbody></table>

#### Block Builder

<table><thead><tr><th width="125.484375">Chain</th><th width="288.10546875">Methods</th><th>Limit</th></tr></thead><tbody><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/block-builder/send-bundle.md">eth_sendBundle</a></li><li><a href="../transaction-submission/block-builder/send-privatetransaction.md">eth_sendPrivateTransaction</a></li></ul></td><td>-</td></tr></tbody></table>

#### Fast

<table><thead><tr><th width="113.1328125">Chain</th><th>Methods</th><th>Limit</th></tr></thead><tbody><tr><td>Solana</td><td><ul><li><a href="../transaction-submission/fast/solana/send-transaction/"><code>Send Transaction</code></a></li><li><a href="../transaction-submission/fast/solana/send-transaction-v2.md"><code>Send Transaction</code> v2</a></li></ul></td><td>Default to 3 TPS</td></tr><tr><td>BSC</td><td><ul><li><a href="../transaction-submission/fast/bsc/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li><li><a href="../transaction-submission/fast/bsc/eth_sendrawtransaction-v2.md"><code>eth_sendRawTransaction</code> v2</a></li></ul></td><td>Default to 10 TPS</td></tr><tr><td>Base</td><td><ul><li><a href="../transaction-submission/fast/base/eth_sendrawtransaction.md"><code>eth_sendRawTransaction</code></a></li></ul></td><td>Default to 10 TPS</td></tr></tbody></table>

