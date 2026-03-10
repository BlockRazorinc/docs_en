# BSC

### Introduction

The BSC Private Mempool delivers private transaction stream data, which is pushed base on the SSE protocol and uniformly in bundle format. Transactions within the data stream are uniformly desensitized, disclosing only transaction fields authorized for release.

Private Mempool can be applied to a variety of scenarios, including backrunning, copy trading, and sniping.

To avoid data interruption due to network fluctuations, it is recommended to establish a reconnection mechanism.



### Endpoint

{% hint style="info" %}
Please keep the domain for subscribing to bundles consistent with the domain for sending bundles. For example, if you subscribe to `https://jp-bscscutum.blockrazor.xyz/stream`, send bundles to `https://jp-bscscutum.blockrazor.xyz`.
{% endhint %}

{% hint style="info" %}
Private data streams vary across regions. It is recommended to subscribe to all three endpoints simultaneously.
{% endhint %}

<table><thead><tr><th width="129.359375">地區</th><th>端點</th></tr></thead><tbody><tr><td>Tokyo</td><td>https://jp-bscscutum.blockrazor.xyz/stream</td></tr><tr><td>New York</td><td>https://us-bscscutum.blockrazor.xyz/stream</td></tr><tr><td>Frankfurt</td><td>https://ger-bscscutum.blockrazor.xyz/stream</td></tr><tr><td>Dublin</td><td>https://ire-bscscutum.blockrazor.xyz/stream</td></tr></tbody></table>



### Authentication

To verify the credential, please set the auth token. An example is as follows:

```json
curl -X GET \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer <token>" \
    --data '{}' \
    https://jp-bscscutum.blockrazor.xyz/stream
```

```
https://jp-bscscutum.blockrazor.xyz/stream?token=<token>
```

The \<token> in the example must be obtained after registering for BlockRazor. The steps are as follows:

1. Go to [https://www.blockrazor.io](https://www.blockrazor.io/) and click on \[Register] in the upper right corner of the webpage, the system will redirect you to the registration page.
2. On the registration page, enter your email and password, then click \[Register], the system will send an account activation email to your mailbox.
3. Go to your mailbox, check the account activation email, and click on the account activation link.
4. After completing the account activation, proceed to log in, check your account information, and copy the auth token.



### Rate Limit

|             | Tier 4 | Tier 3 | Tier 2    | Tier 1    | Tier 0    |
| ----------- | ------ | ------ | --------- | --------- | --------- |
| Data Stream | -      | -      | 2 streams | 2 streams | 2 streams |



### Bundle Type

#### **Raw Bundle**

Raw Bundle refers to the bundle that has not been followed by the strategy transaction. Transactions in Raw Bundle come from two channels.

Transactions submitted through `eth_sendRawTransaction` will be automatically constructed as a bundle by BlockRazor RPC and pushed to Private Mempool. The Raw Bundle in this scenario only contains one transaction;

For the Raw Bundle submitted through `eth_sendMevBundle`, the transactions come from the public mempool or are self-constructed. The Raw Bundle in this scenario can contain up to 50 transactions.

#### Followed Bundle

After the client executes the backrun, coping trading or sniping strategy on Raw Bundle, it can choose to continue to disclose the bundle to Private Mempool to execute the nested backrun strategy. At this time, the bundle disclosed to the Private Mempool is the Followed Bundle, which contains all transactions in Raw Bundle, and one strategy transaction.



### Data Stream Structure

**Bundle**

<table><thead><tr><th width="169">Patameters</th><th width="131">Format</th><th>Remark</th></tr></thead><tbody><tr><td>chainID</td><td>string</td><td>ETH: 1, BSC:56</td></tr><tr><td>hash</td><td>string</td><td>bundle hash, data streams are pushed uniformly in the form of bundles</td></tr><tr><td><a href="bsc.md#tx">txs</a></td><td><a href="bsc.md#tx">[]tx</a></td><td>transactions included in bundle</td></tr><tr><td>nextBlockNumber</td><td>uint64</td><td>the block number where the bundle is going to be included</td></tr><tr><td>maxBlockNumber</td><td>uint64</td><td>the maximum block number valid for this bundle</td></tr><tr><td>proxyBidContract</td><td>string</td><td>proxy contract address of bundle bidding,  biding call for detail can be found in <a data-mention href="/broken/pages/ugvQCt84QW0SIkVonADF">Broken link</a>.</td></tr><tr><td>refundAddress</td><td>string</td><td>input parameter of bidding call, the bidding will be refunded to refundAddress in proportion.</td></tr><tr><td>refundCfg</td><td>int</td><td>input parameter of bidding call</td></tr><tr><td>state</td><td>[]state</td><td>state change of state objects in EVM,   <a href="bsc.md#data-stream-example-including-state">data stream example</a></td></tr></tbody></table>

**txs**

<table><thead><tr><th width="195">Patameters</th><th width="132">Format</th><th>Remark</th></tr></thead><tbody><tr><td>hash</td><td>string</td><td>transaction hash</td></tr><tr><td>from</td><td>string</td><td>sender of the transaction</td></tr><tr><td>to</td><td>string</td><td>receiver of the transaction</td></tr><tr><td>value</td><td>hex</td><td>value being transacted</td></tr><tr><td>nonce</td><td>uint64</td><td>nonce</td></tr><tr><td>calldata</td><td>string</td><td>calldata</td></tr><tr><td>functionSelector</td><td>string</td><td>the first 4 bytes of the contract function signature hash</td></tr><tr><td>logs</td><td><a href="bsc.md#log">[]log</a></td><td>event logs emitted during transaction execution</td></tr></tbody></table>

**log**

<table><thead><tr><th width="199">Patameters</th><th width="132">Format</th><th>Remark</th></tr></thead><tbody><tr><td>address</td><td>string</td><td>the smart contract address that triggered the event</td></tr><tr><td>topics</td><td>[]string</td><td>event log topcis</td></tr><tr><td>data</td><td>string</td><td>storage area for non-index data</td></tr></tbody></table>



#### **state**

{% hint style="info" %}
the default data stream does not contain `state` field, if you need it, please modify the url of RPC Endpoint to [https://jp-bscscutum.blockrazor.xyz/stream?state=true](https://jp-bscscutum.blockrazor.xyz/stream?state=true)
{% endhint %}

<table><thead><tr><th width="208">Patameters</th><th width="123">Format</th><th>Remark</th></tr></thead><tbody><tr><td>"0x7C3b……3cb9E2"</td><td>[]string</td><td>The address of the state object where the data changes, which can be EOA or smart contract</td></tr><tr><td>"0x935b……6cf608"</td><td>string</td><td>the Key of the changed data in state object</td></tr><tr><td>"0x0000……3ffc00"</td><td>string</td><td>the Value of changed data in state object</td></tr></tbody></table>



### Data Stream Example(default)

```json
{
    "chainID":"56" //ETH: 1, BSC:56
    "hash":"0x2ba4c05436d4a48a0ce30341a3164b34b31c091a28ed62618f7b0512aba41f51" // bundle hash
    "txs":[{
          "hash":"0x2ba4c05436d4a48a0ce30341a3164b34b31c091a28ed62618f7b0512aba41f51"
          "from":"0xB4647b856CB9C3856d559C885Bed8B43e0846a47"
          "to":"0x0000000000000000000000000000000000001000"
          "value":"0x1c4eda9192000"
          "nonce":88036
          "calldata":"0xf340fa01000000000000000000000000b4647b856cb9c3856d559c885bed8b43e0846a47"
          "functionSelector":"0xe47d166c"
          "logs":[
              {
                "address": "0x6c1bcf1b99d9f0819459dad661795802d232437e",
                "topics": ["0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67", "0x0000000000000000000000000000000000000000000000000000000000000000", "0x0000000000000000000000000000000000000000000000000000000000000000"],
                "data": "0x"
              }
              {
                "address": "0x6c1bcf1b99d9f0819459dad661795802d232437e",
                "topics": ["0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67", "0x0000000000000000000000000000000000000000000000000000000000000000", "0x0000000000000000000000000000000000000000000000000000000000000000"],
                "data": "0x"
              }
          ]
    }]
    "nextBlockNumber":39177941  //the block number where the bundle is going to be included
    "maxBlockNumber":39177941  //the maximum block number valid for this bundle
    "proxyBidContract":"0x74Ce839c6aDff544139f27C1257D34944B794605" //bidding contract address, call the contract's proxyBid method to bid
    "refundAddress":"0x6c1bcf1b99d9f0819459dad661795802d232437e", //the bidding amount will be refunded to refundAddress in proportion
    "refundCfg":10380050 //refund configuration
}
```



### Data Stream Example(including state)

{% hint style="info" %}
The default data stream does not contain `state` field, if you need to obtain it, please modify the url of RPC Endpoint to [https://bsc.blockrazor.xyz/stream?state=true](https://bsc.blockrazor.xyz/stream?state=true)
{% endhint %}

```json
{
    "chainID":"56" //ETH: 1, BSC:56
    "hash":"0x2ba4c05436d4a48a0ce30341a3164b34b31c091a28ed62618f7b0512aba41f51" // bundle hash
    "txs":[{
          "hash":"0x2ba4c05436d4a48a0ce30341a3164b34b31c091a28ed62618f7b0512aba41f51"
          "from":"0xB4647b856CB9C3856d559C885Bed8B43e0846a47"
          "to":"0x0000000000000000000000000000000000001000"
          "value":"0x1c4eda9192000"
          "nonce":88036
          "calldata":"0xf340fa01000000000000000000000000b4647b856cb9c3856d559c885bed8b43e0846a47"
          "functionSelector":"0xe47d166c"
          "logs":[
              {
                "address": "0x6c1bcf1b99d9f0819459dad661795802d232437e",
                "topics": ["0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67", "0x0000000000000000000000000000000000000000000000000000000000000000", "0x0000000000000000000000000000000000000000000000000000000000000000"],
                "data": "0x"
              }
              {
                "address": "0x6c1bcf1b99d9f0819459dad661795802d232437e",
                "topics": ["0xc42079f94a6350d7e6235f29174924f928cc2ac818eb64fed8004e115fbcca67", "0x0000000000000000000000000000000000000000000000000000000000000000", "0x0000000000000000000000000000000000000000000000000000000000000000"],
                "data": "0x"
              }
          ]
    }]
    "nextBlockNumber":39177841  //the block number where the bundle is going to be included
    "maxBlockNumber":39177941  //the maximum block number valid for this bundle
    "proxyBidContract":"0x74Ce839c6aDff544139f27C1257D34944B794605" //bidding contract address, call the contract's proxyBid method to bid
    "refundAddress":"0x6c1bcf1b99d9f0819459dad661795802d232437e", //the bidding amount will be refunded to refundAddress in proportion
    "refundCfg":10380050 //refund configuration
    "state": { //state change of state objects
	"0x7C3b00CB3B40Cc77d88329A58574E29cFA3cb9E2": { //The address of the state object where the data changes, which can be EOA or smart contract
	      "0x935b605129a438014d6ae0692623c5e1fbf83d5a631f5a0f8489a301966cf608": "0x00000000000000000000000000000000000000000000010c86a7e418723ffc00"
	      //"the Key of the changed data in state object":"the Value of changed data in state object"
	      }
      }
}
```

