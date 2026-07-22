# eth\_sendBatch

{% hint style="info" %}
Robinhood Chain RPC is not currently available to the public. If you would like to integrate with it, please [contact us](https://discord.gg/qqJuwRb8Nh).
{% endhint %}

`eth_sendBatch` is a transaction batch sending interface provided by BlockRazor for Robinhood Chain. Users can use this method to send signed raw transactions in batches to the chain with low latency. Currently, HTTPS protocol is supported.

A batch has a maximum transaction capacity of 10 transactions, which are sent sequentially to Robinhood's official sequencer every 5ms. It's important to note that batches are not atomic and there is no guarantee that the final on-chain order will match the expected request order.

### What is Robinhood Chain <a href="#what-is-robinhood-chain" id="what-is-robinhood-chain"></a>

Robinhood Chain is a Ethereum Layer 2 built on Arbitrum, optimized for tokenized real-world assets including equities and ETFs, enabling 24/7 onchain trading and self-custody.

Robinhood Chain Website：[https://robinhood.com/us/en/chain/](https://robinhood.com/us/en/chain/)

Robinhood Chain Stats：[https://robinhoodchain.blockscout.com/stats](https://robinhoodchain.blockscout.com/stats)

### Request parameters

<table><thead><tr><th width="123.7890625">Parameters</th><th width="122.76953125">Mandatory</th><th width="101.30859375">Format</th><th width="203.80078125">Example</th><th>Description</th></tr></thead><tbody><tr><td>-</td><td>Mandatory</td><td>String[]</td><td>["0x…9c","0x…6a"]</td><td>Signed raw transactions</td></tr></tbody></table>

### Request Example

{% tabs %}
{% tab title="HTTPS" %}
```bash
curl https://robinhood.blockrazor.io \
  -H 'content-type: application/json' \
  -H 'Authorization: Bearer <auth-token>' \
  --data '{
  "jsonrpc": "2.0",
  "id": "1",
  "method": "eth_sendBatch",
  "params": ["0x…9c","0x…6a"]
}'
```
{% endtab %}
{% endtabs %}

### Response Example

```json
{
 "jsonrpc":"2.0",
 "id":"1",
 "result":"0xa06b……f7e8ec" // batch hash
}‍
```

```json
{
  "jsonrpc":"2.0",
  "id":"1",
  "error":{
    "code":-32000,
    "message":"auth is invalid"
    }
}
```

