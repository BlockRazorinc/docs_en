# Utilize Dedicate Node

### 1. Get the endpoint

<figure><img src="../../../.gitbook/assets/image (16).png" alt="" width="563"><figcaption><p><a href="https://www.blockrazor.io/#/login">Log in</a> to the Portal, go to 【Dedicate Node】 to get the endpoint</p></figcaption></figure>

### 2. Calling JSON RPC methods

#### Standard JSON RPC methods

The standard JSON RPC method of BSC Dedicate Node (Geth) is fully compatible with Ethereum Geth. For specific calling methods, please refer to [https://ethereum.org/en/developers/docs/apis/json-rpc/#json-rpc-methods](https://ethereum.org/en/developers/docs/apis/json-rpc/#json-rpc-methods)



#### Custom JSON RPC Methods

BSC Dedicate Node (Geth) supports bundle simulation. The method name is `eth_simulateBundles`. The request and return examples are as follows:

**Request**

```
curl -X POST <dedicate node url> \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "eth_simulateBundles",
    "params": [
      [
        {
          "from": "0x03Ae1e3082dD5E338e8Ae8572A34bcdF8be40362",
          "to": "0x55d398326f99059fF775485246999027B3197955",
          "data": "0x18160ddd",
          "gas": "0x100000"
        }
      ],
      "latest" // Specifies the block height or status to be simulated. latest indicates the latest produced block.

    ]
  }'
```



**Response**

```
{"jsonrpc":"2.0","id":1,"result":[{"return":"0x","gasUsed":21160}]}
```

```
{"jsonrpc":"2.0","id":1,"result":[{"return":"0x","gasUsed":21070,"revertReason":"execution reverted"}]}
```

```
{"jsonrpc":"2.0","id":1,"result":[{"return":"0x","gasUsed":0,"error":"err: intrinsic gas too low: have 0, want 21000 (supplied gas 0)"}]}
```



