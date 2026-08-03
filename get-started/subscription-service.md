---
description: >-
  This section introduces the pricing for subscription services (personalized
  and packages), and the services that new registered users can enjoy with zero
  minimum purchase requirem
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Subscription Service

{% hint style="info" %}
BlockRazor's pricing system now supports purchasing individual services across chains, purchasing packages at a lower price, and purchasing on a daily basis.
{% endhint %}

### Personalized

{% tabs %}
{% tab title="BSC" %}
<table data-search="false"><thead><tr><th width="157.33203125">Service</th><th width="201.1640625">Description</th><th>Price</th><th>Action</th></tr></thead><tbody><tr><td><a href="../transaction-submission/fast/bsc/broadcast-tx.md">Broadcast Tx</a></td><td>Propagating transactions and transaction batches with low latency</td><td>$50 / day<br>$500 / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_fast_tx&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../streams/mempool/bsc/public-mempool.md">Public Mempool</a></td><td>Subscribe to mempool transactions with low latency</td><td>$30 / day<br>$300 / stream / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_public_mempool&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../streams/mempool/bsc/private-mempool.md">Private Mempool</a></td><td>Subscribe to BlockRazor RPC orderflow</td><td>$100 / day<br>$1000 / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_private_mempool&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../streams/block-stream/bsc/newblocks.md">Block Stream</a></td><td>Subscribe to blocks with low latency</td><td>$50 / day<br>$500 / stream / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_block_stream&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../streams/node-stream/bsc/full-node-synchronization.md">Node Stream</a></td><td>Low-latency synchronized world state</td><td>$80 / day<br>$800 / enode / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_enode&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../streams/network-fee-stream/bsc/getgaspricestream.md">Network Fee Stream</a></td><td>Obtain BSC gas price data</td><td>$30 / day<br>$300 / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_fee_stream&#x26;billing=day" class="button primary small">Subscribe</a></td></tr><tr><td><a href="../transaction-submission/block-builder/trace-bundle.md">Bundle Tracing &#x26; Explorer</a></td><td>Tracing and explore bundle of Block Builder</td><td>$150 / day<br>$1500 / month</td><td><a href="https://blockrazor.io/#/login?redirect=pricing&#x26;purchaseMode=personalized&#x26;chain=bsc&#x26;serviceId=bsc_bundle_tracing&#x26;billing=day" class="button primary small">Subscribe</a></td></tr></tbody></table>
{% endtab %}

{% tab title="Solana" %}
<table><thead><tr><th width="137.625">Service</th><th width="152.546875">Description</th><th width="230.265625">Monthly Purchase</th><th>Daily Purchase</th></tr></thead><tbody><tr><td><a href="../streams/block-stream/solana/shred-stream.md">Shred Stream</a></td><td>Low-latency transmission of shreds</td><td>$500 / stream / month</td><td>$50 / stream / day</td></tr><tr><td><a href="../streams/block-stream/solana/geyser-stream/">Geyser Stream</a></td><td>Real-time transmission of on-chain data from Solana, including accounts, slots, blocks, and transactions.</td><td>5 TiB - $250 / month<br>10 TiB - $500 / month<br>50 TiB - $250 / month<br>100 TiB - $4750 / month<br>150 TiB - $6750 / month<br>200 TiB - $8500 / month<br>250 TiB - $10000 / month</td><td>-</td></tr><tr><td><a href="../streams/network-fee-stream/solana/get-transactionfee.md">Network Fee Stream</a></td><td>Get Solana priority fee and tip data</td><td>$300 / month</td><td>$30 / day</td></tr></tbody></table>
{% endtab %}

{% tab title="Ethereum" %}
<table><thead><tr><th width="134.33984375">Service</th><th width="250.5390625">Description</th><th>Monthly Purchase</th><th>Daily Purchase</th></tr></thead><tbody><tr><td><a href="../transaction-submission/fast/ethereum/broadcast-tx.md">Broadcast Tx</a></td><td>Propagating transactions and transaction batches with low latency</td><td>$500 / month</td><td>$50 / day</td></tr><tr><td><a href="../streams/mempool/ethereum/public-mempool.md">Public Mempool</a></td><td>Subscribe to mempool transactions with low latency</td><td>$300 / stream / month</td><td>$30 / day</td></tr><tr><td><a href="../streams/block-stream/ethereum/newblocks.md">Block Stream</a></td><td>Subscribe to blocks with low latency</td><td>$500 / stream / month</td><td>$50 / day</td></tr><tr><td><a href="../streams/node-stream/ethereum/cl-el-client-sync.md">Node Stream</a></td><td>Low-latency synchronized world state</td><td>$800 / client / month</td><td>$80 / day</td></tr></tbody></table>
{% endtab %}

{% tab title="Base" %}
<table><thead><tr><th width="133.1015625">Service</th><th>Description</th><th width="150.23828125">Monthly Purchase</th><th>Daily Purchase</th></tr></thead><tbody><tr><td><a href="../streams/block-stream/base/get-flashblockstream/">FlashBlock Stream</a></td><td>Low-latency acquisition of Base FlashBlock data</td><td>$250 / stream / month</td><td>$25 / stream / day</td></tr><tr><td><a href="../streams/block-stream/base/get-blockstream.md">Block Stream</a></td><td>Low-latency acquisition of Base Block data</td><td>$300 / stream / month</td><td>$30 / stream / day</td></tr><tr><td><a href="../transaction-submission/rpc/base/eth_sendrawtransaction.md">RPC-Send Tx</a></td><td>Low latency and high TPS for sending base transactions on-chain</td><td>$1000 / month</td><td>$100 / stream / day</td></tr></tbody></table>
{% endtab %}

{% tab title="General" %}
<table><thead><tr><th width="129.40234375">Service</th><th width="192.92578125">Description</th><th>Monthly Purchase</th><th>Daily Purchase</th></tr></thead><tbody><tr><td>Dedicated Channel</td><td>Dedicated technical support</td><td>$1000 / month</td><td>$100 / day</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Package

{% hint style="info" %}
Compared to purchasing individual services, users can complete a package purchase at a lower price through the Package. Currently, the Package mainly includes the BSC service, with a total subscription price of **$1250/month**. Specific services are as follows:
{% endhint %}

<table><thead><tr><th width="257.74609375">Service</th><th width="96.99609375">Quota</th><th>Description</th></tr></thead><tbody><tr><td><a href="../streams/mempool/bsc/public-mempool.md">Public Mempool - BSC</a><br><a href="../streams/mempool/ethereum/public-mempool.md">Public Mempool - Ethereum</a></td><td>2</td><td>Low-latency subscription to BSC and Ethereum public mempool transaction data, with subscription quota shared across chains.</td></tr><tr><td><a href="../streams/block-stream/bsc/newblocks.md">Block Stream - BSC</a><br><a href="../streams/block-stream/ethereum/newblocks.md">Block Stream - Ethereum</a></td><td>2</td><td>Low-latency subscription to BSC and Ethereum block data, with subscription quota shared across chains.</td></tr><tr><td><a href="../streams/node-stream/bsc/full-node-synchronization.md">Node Stream - BSC</a><br><a href="../streams/node-stream/ethereum/cl-el-client-sync.md">Node Stream - Ethereum</a></td><td>1</td><td>Low-latency synchronization of world state between BSC and Ethereum, and cross-chain sharing of synchronization quotas.</td></tr><tr><td><a href="../transaction-submission/block-builder/call-bundle.md">Call Bundle</a></td><td>1</td><td>Submit a request to Block Builder to receive bundle simulation results</td></tr><tr><td><a href="../transaction-submission/block-builder/fast-submit.md">Fast Submit</a></td><td>1</td><td>Submit transactions to Block Builder with lower latency and higher stability</td></tr><tr><td><a href="../streams/mempool/bsc/tx-trace.md">Tx Trace</a></td><td>1</td><td>Monitoring transaction propagation paths and cross-regional latency distribution</td></tr></tbody></table>

### Discount

The relationship between discounts and subscription periods is as follows:

<table><thead><tr><th width="314.41796875">Periods</th><th width="328.90234375">Discount</th></tr></thead><tbody><tr><td>1 month</td><td>-</td></tr><tr><td>3 months</td><td>5% off</td></tr><tr><td>6 months</td><td>10% off </td></tr><tr><td>9 months</td><td>15% off</td></tr><tr><td>12 months</td><td>20% off</td></tr></tbody></table>

### FAQ

<details>

<summary>Can the Navigator Package and Personalized Services be ordered at the same time?</summary>

They can be ordered at the same time.

</details>

<details>

<summary>What does the data stream limit refer to in the optional services?</summary>

Data stream service quota refers to the number of gRPC data streams that are allowed to connect. The quota is shared across multiple regions. For example, if you purchase one Public Mempool, only one data stream connection is allowed in all regions.

</details>

<details>

<summary>What does "shared quota" mean in the Navigator Package?</summary>

In the Navigator Package, Public Mempool, Block Stream, and Node Stream share data stream quotas on BSC and Ethereum. For example, if you purchase the Navigator Package and obtain 2 Public Mempool quotas, you are allowed to subscribe to a total of 2 data streams on BSC and Ethereum. If you have already subscribed to 2 BSC Public Mempools, you cannot subscribe to Public Mempools on Ethereum.

</details>

