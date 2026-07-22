# eth\_sendRawTransaction

{% hint style="info" %}
Robinhood Chain RPC is not currently available to the public. If you would like to integrate with it, please [contact us](https://discord.gg/qqJuwRb8Nh).
{% endhint %}

`eth_sendRawTransaction` is a transaction sending interface provided by BlockRazor for Robinhood Chain. Users can use this method to send signed raw transactions to the chain with low latency. Currently, HTTPS protocol is supported.

### What is Robinhood Chain <a href="#what-is-robinhood-chain" id="what-is-robinhood-chain"></a>

Robinhood Chain is a Ethereum Layer 2 built on Arbitrum, optimized for tokenized real-world assets including equities and ETFs, enabling 24/7 onchain trading and self-custody.

Robinhood Chain Website：[https://robinhood.com/us/en/chain/](https://robinhood.com/us/en/chain/)

Robinhood Chain Stats：[https://robinhoodchain.blockscout.com/stats](https://robinhoodchain.blockscout.com/stats)

### Benchmark

We deployed test clients across AWS regions in Frankfurt, Ohio, and Japan, and sent 50 pairs of transactions with identical nonces to both the corresponding regional BlockRazor endpoints and the official RPC endpoints. Within each transaction pair, all parameters were kept exactly the same except for the recipient address, which was used to distinguish between the two submission channels.

Performance was evaluated by comparing the ratio of transactions that were ultimately included through each channel. A higher on-chain inclusion rate indicates faster transaction propagation and execution performance. The benchmark results are shown below.

<table><thead><tr><th width="174.3359375">Region</th><th>BlockRazor Inclusion Rate</th><th>Robinhood Inclusion Rate</th></tr></thead><tbody><tr><td>Frankfurt</td><td>88%</td><td>12%</td></tr><tr><td>Ohio</td><td>50%</td><td>50%</td></tr><tr><td>Japan</td><td>96%</td><td>4%</td></tr></tbody></table>

### Request parameters

<table><thead><tr><th width="123.7890625">Parameters</th><th width="122.76953125">Mandatory</th><th width="101.30859375">Format</th><th width="106">Example</th><th>Description</th></tr></thead><tbody><tr><td>-</td><td>Mandatory</td><td>String</td><td>"0x…4b"</td><td>Signed raw transaction</td></tr></tbody></table>

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
  "method": "eth_sendRawTransaction",
  "params": ["0x…9c"]
}'
```
{% endtab %}
{% endtabs %}

### Response Example

```json
{
 "jsonrpc":"2.0",
 "id":"1",
 "result":"0xa06b……f7e8ec"
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

