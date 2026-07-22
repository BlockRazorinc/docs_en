---
hidden: true
---

# Send Tx

`eth_sendRawTransaction` is a transaction sending interface provided by BlockRazor for Robinhood Chain. Users can use this method to send signed raw transactions to the chain with low latency. Currently, HTTPS protocol is supported.

Compared to [`eth_sendRawTransaction`](eth_sendrawtransaction.md), `Send Tx` undergo pre-flight checks before being sent to the Robinhood Chain official sequencer, including but not limited to whether the nonce is correct, whether the balance is sufficient, and whether contract execution has been reverted.

### Price

| User Type            | Limit      | Price |
| -------------------- | ---------- | ----- |
| New registered users | 20 Tx / 1s | 免費    |

### Endpoint

<table><thead><tr><th width="152.078125">Region</th><th>Endpoint</th></tr></thead><tbody><tr><td>Global</td><td>https://robinhood.blockrazor.io</td></tr><tr><td>Frankfurt</td><td>https://eu.robinhood.blockrazor.io</td></tr><tr><td>Ohio</td><td>https://us.robinhood.blockrazor.io</td></tr><tr><td>Japan</td><td>https://ap.robinhood.blockrazor.io</td></tr></tbody></table>

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
  "method": "sendTx",
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
    "message":"nonce too low: next nonce 57, tx nonce 56"
    }
}
```

