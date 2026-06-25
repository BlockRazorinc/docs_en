---
hidden: true
---

# Send BackBundle

### Introduction

This interface is used to receive bundle which is put at the block tail, allowing all transactions within the bundle to have a gas price of 0 gwei. Currently, this interface only supports the Virginia endpoint, it is recommended to deploy your service nearby.

### Endpoint

https://virginia.builder.blockrazor.io

### Request Parameter

<table><thead><tr><th width="136.6875">Parameters</th><th width="118.74609375">Mandatory</th><th width="136">Format</th><th width="124">Example</th><th>Description</th></tr></thead><tbody><tr><td>txs</td><td>true</td><td>array[hex]</td><td>["0x…4b"]</td><td>signed raw transaction</td></tr><tr><td>blockNumber</td><td>true</td><td>uint64</td><td>106211355</td><td>The target block in which the bundle is expected to be included</td></tr></tbody></table>

### Request Example

```json
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: <YOUR_TOKEN>" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_sendBackBundle",
    "params": [
      {
        "txs": ["0x...4b"],
        "blockNumber": 106211355
      }
    ]
  }' \
  https://virginia.builder.blockrazor.io
```

### Response Example

Normal

```json
{
 "jsonrpc":"2.0",
 "id":"1",
 "result":null
}‍
```

Abnormal

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "error": {
    "code": -32000,
    "message": "bundle missing blockNumber"
  }
}
```
