# Searcher

### Introduction

Searchers can subscribe to transactions from the [Private Mempool](../../../streams/mempool/private-mempool/) to execute backrun strategies, and then send bid to BlockRazor RPC to win the backrun auction.&#x20;

Additionally, searchers can skip bundle subscriptions and directly send bundles to BlockRazor RPC. With the network acceleration service of the high-performance network, BlockRazor RPC can forward bundles to builders with minimal latency, eliminating the need to repeatedly connect to builder interfaces.



### RPC Endpoint

{% hint style="info" %}
Please keep the domain for subscribing to the bundle consistent with the domain for sending the bundle. For example, if subscribing to <mark style="color:$info;">https://jp-ethscutum.blockrazor.xyz/stream</mark>, then send the bundle to <mark style="color:$info;">https://jp-ethscutum.blockrazor.xyz</mark>
{% endhint %}

<table><thead><tr><th width="149.453125">Region</th><th>Endpoint</th></tr></thead><tbody><tr><td>Tokyo</td><td>https://jp-ethscutum.blockrazor.xyz</td></tr><tr><td>New York</td><td>https://us-ethscutum.blockrazor.xyz</td></tr></tbody></table>



### eth\_sendBid

{% hint style="info" %}
To protect private transactions, `eth_sendBid` is restricted to designated Searchers. Please [contact](https://discord.com/invite/qqJuwRb8Nh) us if you need to send a bid.
{% endhint %}

#### Request Parameter

<table><thead><tr><th width="121.43359375">Parameter</th><th width="123.98828125">Mandatory</th><th width="97.12109375">Format</th><th width="119.37890625">Example</th><th>Remark</th></tr></thead><tbody><tr><td>txs</td><td>Mandatory</td><td>[]string</td><td>["tx_hash", "rawTxHex"]</td><td><code>tx_hash</code> refers to the originator transaction in the  <a href="../../../streams/mempool/private-mempool/">Private Mempool</a>, while <code>rawTxHex</code> is the backrun transaction being constructed.<br>If the backrun target is a bundle, please fill in all <code>tx_hash</code> values from the bundle.</td></tr><tr><td>blockNumber</td><td>Optional</td><td>hex string</td><td>"0x102286B"</td><td>A hex-encoded block number indicating the latest valid block for the bundle. The default value is the current block number + 100.</td></tr></tbody></table>

#### Bid **mechanism**

BlockRazor will replace the `tx_hash` in the Bid with `rawTxHex`, and after adding `refundPercent` and `refundRecipient`, immediately forward it to the Builder for block inclusion.&#x20;

From the Builder's perspective, the Bid's value is determined by the backrun transaction’s `priority fee + coinbase.transfer()`. Since the `refundPercent` for the same originator transaction remains consistent, the Bid with the highest total value will be successfully included.

#### Request Example

**Backrun Originator Transaction**

```bash
curl https://eth.blockrazor.xyz \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  --data '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_sendBid",
    "params": [
      {
        "txs": [
          "0x3a3c086bad1e765076986814939d2be70399e85ff75e4da8ec730aaf6ce3fea1",
          "0x02f86d0182149c808411e1a300830484e294fef10de0823f58df4f5f24856ab4274ededa6a5c8084c179306cc001a075d1f8fea39352c2da065aeef85be4b24789953f57a62ca7ad29b45bfc1e362aa043de44543083d0dafb80eaedd5764d6ef03336ff028ef02f238bccd5dfa9ece9"
        ],
        "blockNumber": "0x102286B"
      }
    ]
  }'
```

**Backrun Originator Bundle**

```bash
curl https://eth.blockrazor.xyz \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  --data '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_sendBid",
    "params": [
      {
        "txs": [
          "0x3a3c086bad1e765076986814939d2be70399e85ff75e4da8ec730aaf6ce3fea1",
          "0x47816242f30167d1525a98801355f49370fc83049cb070d5d3ae9fd6c83d2d9d",
          "0x02f86d0182149c808411e1a300830484e294fef10de0823f58df4f5f24856ab4274ededa6a5c8084c179306cc001a075d1f8fea39352c2da065aeef85be4b24789953f57a62ca7ad29b45bfc1e362aa043de44543083d0dafb80eaedd5764d6ef03336ff028ef02f238bccd5dfa9ece9"
        ],
        "blockNumber": "0x102286B"
      }
    ]
  }'
```



### eth\_sendBundle

Searchers can also act as project builders to send raw bundles. For details, please refer to [Project Builder](project-builder.md).



