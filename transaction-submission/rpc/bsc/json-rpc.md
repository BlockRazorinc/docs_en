# JSON-RPC

### eth\_sendRawTransaction

&#x20;`eth_sendRawTransaction` of BlockRazor RPC is compatible with native JSON-RPC methods and requires no additional modifications. If you need to modify parameters such as hint, refund address and revert protection, you can configure the dedicated RPC in the [portal](https://www.blockrazor.io/#/login)

#### Request parameters

<table><thead><tr><th width="124">Parameters</th><th width="127">Mandatory</th><th width="110">Format</th><th width="180">Example</th><th>Remark</th></tr></thead><tbody><tr><td>-</td><td>Mandatory</td><td>bytes</td><td>"0xd46e……445675"</td><td>raw tx</td></tr></tbody></table>

#### Request Example

```json
curl -X POST -H "Content-Type: application/json" --data '{
    "id": 1,
    "jsonrpc": "2.0",
    "method": "eth_sendRawTransaction",
    "params": [
        "0xd46e……445675"
    ]
}' https://bsc.blockrazor.xyz
```

#### Response Example

**normal**

```json
{
  "id":1,
  "jsonrpc": "2.0",
  "result": "0xe670……527331"
}
```

**abnormal**

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "error": {
	"code": -32000,
	"message": "rlp: element is larger than containing list"
  }
}
```



### eth\_sendMevBundle <a href="#eth_sendmevbundle" id="eth_sendmevbundle"></a>

Bundle Submission is supported in BlockRazor RPC, please refer to [Bundle](../../bundle/bsc/project-builder.md)



### scutum\_queryTxProcessStatus

`scutum_queryTxProcessStatus` is used to query the real-time process status of transactions sent to BlockRazor RPC. It is currently available on BSC.

#### Request Example

```json
curl -X POST -H "Content-Type: application/json" --data'{
	"id": 1,
	"jsonrpc": "2.0",
	"method": "scutum_queryTxProcessStatus",
	"params": ["0xf84a……e54284"]
}'<ETH_NODE_URL>
```

#### Response Example

**Normal**

```json
{
  "jsonrpc": "2.0",
  "result": "{"msg\":\"tx is included on chain\",\"status\":\"included\"}",
  "id": "1"
} // the tx is executed on chain, success or reverted
```

```json
{
  "jsonrpc": "2.0",
  "result": "{"msg\":\"tx is expired and discarded\",\"status\":\"expired\"}",
  "id": "1"
} // 100 blocks has passed since submission of the tx
```

```json
{
  "jsonrpc": "2.0",
  "result": "{"msg\":\"nonce too high\",\"status\":\"pending\"}",
  "id": "1"
} // the tx is queued since the nonce is too high
```

```json
{
  "jsonrpc": "2.0",
  "result": "{"msg\":\"tx is pending\",\"status\":\"pending\"}",
  "id": "1"
} // the tx is being processed by Scutum
```

```json
{
  "jsonrpc": "2.0",
  "result": "{"msg\":\"simulation error: xxxxxxx\",\"status\":\"failed\"}",
  "id": "1"
} // the tx failed to be processed by Scutum due to the simulation error
```

**Abnomal**

```json
{
  "jsonrpc": "2.0",
  "error": "{\"code\":-32000,\"message\":\"tx not found\"}",
  "id": "1"
}  //the tx has not been sent to Scutum or has exceeded the Scutum processing time limit
```



### Other JSON-RPC Methods

BlockRazor RPC supports standard JSON-RPC method, you can refer to [https://ethereum.org/zh/developers/docs/apis/json-rpc/#json-rpc-methods](https://ethereum.org/zh/developers/docs/apis/json-rpc/#json-rpc-methods)
