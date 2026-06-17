---
description: >-
  Introduction to eth_sendRawTransaction of BlockRazor BSC Fast mode and
  integration methods
---

# eth\_sendRawTransaction

### Introduction

`eth_sendRawTransaction` is a Fast mode transaction sending interface provided by BlockRazor for BSC. It is compatible with the standard `eth_sendRawTransaction`  method and is used to send signed transactions with lower latency.

Transactions sent to Fast mode `eth_sendRawTransaction`are not broadcast through the public mempool, thus improving sending speed while preventing transactions from being exposed during public propagation.

{% hint style="info" %}
Fast Mode is not tied to the subscription plan, but each transaction sent in Fast Mode must include a tip sent to the address `0x9D70AC39166ca154307a93fa6b595CF7962fe8e5`. The minimum tip amount is the greater of 0.000025 BNB or Transaction Fee \* 5%.
{% endhint %}

### Endpoint

{% tabs %}
{% tab title="General" %}
http://bsc-fast.blockrazor.io
{% endtab %}

{% tab title="Geographic" %}
<table><thead><tr><th width="146.0703125">Region</th><th>Domain</th></tr></thead><tbody><tr><td>Frankfurt</td><td>http://frankfurt.bsc-fast.blockrazor.io</td></tr><tr><td>Japan</td><td>http://japan.bsc-fast.blockrazor.io</td></tr><tr><td>Virginia</td><td>http://virginia.bsc-fast.blockrazor.io</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Rate Limit

Fast Mode is not tied to the subscription plan, the rate limit default to 10 TPS for all users. Please contact us if you require an increase in your TPS limit.

### Request

```json
curl http://bsc-fast.blockrazor.io \
  -X POST \
  -H "Authorization: Bearer <auth>" \
  -H "Content-Type: application/json" \
  --data '
    {
    "jsonrpc": "2.0",
    "method": "eth_sendRawTransaction",
    "params": [
      "Signed Transaction"
    ],
    "id": 1
  }
  '
```

### Response

**Normal**

```json
{
 "jsonrpc":"2.0",
 "id":"1",
 "result":"0xa06b……f7e8ec"
}‍
```

**Abnormal**

```json
{
  "jsonrpc":"2.0",
  "id":"1",
  "error":{
    "code":-32000,
    "message":"Tip verification failed"
    }
}
```

### Keep Alive <a href="#keep-alive" id="keep-alive"></a>

Please send a POST request to the health check endpoint to keep the connection alive. We recommend sending a request every 10 seconds. Below is a request example:

{% tabs %}
{% tab title="Curl" %}
```json
curl -X POST 'http://bsc-fast.blockrazor.io/health' \
-H "Content-Type: application/json" \
-d ""
```
{% endtab %}
{% endtabs %}
