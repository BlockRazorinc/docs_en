# Base

### Introduction

The Fast Mode leverages BlockRazor's global high-performance network to achieve the lowest latency for transaction inclusion, making it suitable for users who have extreme requirements for transaction inclusion speed. The transaction submission method for Fast Mode is compatible with `eth_sendRawTransaction`.

{% hint style="info" %}
Fast Mode is not tied to the subscription plan, but each transaction sent in Fast Mode must include a tip sent to the address `0x9D70AC39166ca154307a93fa6b595CF7962fe8e5`. The minimum tip amount is the greater of 0.000003 ETH or MaxPriorityFee \* 5%.
{% endhint %}



### Endpoint

http://base-fast.blockrazor.io



### Rate Limit

Fast Mode is not tied to the subscription plan, the rate limit default to 10 TPS for all users. Please contact us if you require an increase in your TPS limit.



### Request

```json
curl http://base-fast.blockrazor.io \
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
 "result":"0xa06b……f7e8ec"  // 交易哈希
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

