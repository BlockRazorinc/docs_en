# sui\_executeTransactionBlock

### Introduction

The Fast Mode leverages BlockRazor's global high-performance network to achieve the lowest latency for transaction inclusion, making it suitable for users who have extreme requirements for transaction inclusion speed.

The transaction submission method of Fast Mode supports HTTP and gRPC. The HTTP is compatible with [`sui_executeTransactionBlock`](https://docs.sui.io/sui-api-ref#sui_executetransactionblock)and the gRPC is compatible with [`sui_rpc_v2_transaction-execution-service-proto`](https://docs.sui.io/references/fullnode-protocol#sui_rpc_v2_transaction-execution-service-proto) .

{% hint style="info" %}
Fast Mode is not tied to the subscription plan, but each transaction sent in Fast Mode must include a tip. The minimum tip amount is the greater of 0.001 SUI or Gas Budget × 0.05 SUI.&#x20;

Tip Method: Integrate the BlockRazor SDK in [TS](ts.md) or [Go](go.md), and invoke the `AddTip` method.
{% endhint %}



### Endpoint

http://sui-fast.blockrazor.io



### Rate Limit

Fast Mode is not tied to the subscription plan, the rate limit default to 10 TPS for all users. Please [contact](https://discord.com/invite/qqJuwRb8Nh) us if you require an increase in your TPS limit.



### Request Example

* [TS](ts.md)
* [Go](go.md)

