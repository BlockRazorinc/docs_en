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

Bundle Submission is supported in BlockRazor RPC, please refer to [Bundle](../../bundle/ethereum/project-builder.md)



### Other JSON-RPC Methods

BlockRazor RPC supports standard JSON-RPC method, you can refer to [https://ethereum.org/zh/developers/docs/apis/json-rpc/#json-rpc-methods](https://ethereum.org/zh/developers/docs/apis/json-rpc/#json-rpc-methods)

