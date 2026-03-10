# Send Transaction

## Introduction <a href="#jie-shao" id="jie-shao"></a>

{% hint style="warning" %}
Solana's transaction sending service is not bound to the subscription plan, with rate limit default to 1 TPS. API key could be required from [Authentication](../../../../authentication.md). If you need to increase the TPS limit, please [contact](https://discord.com/invite/qqJuwRb8Nh) us and we will handle it as soon as possible.
{% endhint %}

BlockRazor achieves subsecond-level transaction inclusion based on globally distributed high-performance network and high-quality SWQoS(see the [Benchmark](https://www.blockrazor.io/#/blogs/20250801Benchmarking)), and also provides multiple modes such as sandwich mitigation.

`Send Transaction` is used to send signed transaction on Solana based on HTTP and gRPC.



## Endpoint <a href="#xian-liu" id="xian-liu"></a>

**HTTP**

<table><thead><tr><th width="135.50390625">Region</th><th>URL</th></tr></thead><tbody><tr><td>Frankfurt</td><td>http://frankfurt.solana.blockrazor.xyz:443/sendTransaction</td></tr><tr><td>New York</td><td>http://newyork.solana.blockrazor.xyz:443/sendTransaction</td></tr><tr><td>Tokyo</td><td>http://tokyo.solana.blockrazor.xyz:443/sendTransaction</td></tr><tr><td>Amsterdam</td><td>http://amsterdam.solana.blockrazor.xyz:443/sendTransaction</td></tr><tr><td>London</td><td>http://london.solana.blockrazor.xyz:443/sendTransaction</td></tr></tbody></table>



#### gRPC

<table><thead><tr><th width="134.9765625">Region</th><th>URL</th></tr></thead><tbody><tr><td>Frankfurt</td><td>frankfurt.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>New York</td><td>newyork.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Tokyo</td><td>tokyo.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Amsterdam</td><td>amsterdam.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>London</td><td>london.solana-grpc.blockrazor.xyz:80</td></tr></tbody></table>



## Rate Limit <a href="#xian-liu" id="xian-liu"></a>

{% hint style="info" %}
Solana's transaction sending service is no longer bound to the subscription plan. API key could be required from [Authentication](../../../../authentication.md). If you need to increase the TPS limit, please [contact](https://discord.com/invite/qqJuwRb8Nh) us and we will handle it as soon as possible.
{% endhint %}



## Transaction Construction Example <a href="#jiao-yi-gou-jian-dai-ma-shi-li" id="jiao-yi-gou-jian-dai-ma-shi-li"></a>

* [Go](go.md)
* [Rust](rust.md)
* [JS](js.md)



## Request Parameter

<table><thead><tr><th width="111.44921875">Parameters</th><th width="115.421875">Mandatory</th><th width="109.98046875">Example</th><th>Description</th></tr></thead><tbody><tr><td>transaction</td><td>Mandatory</td><td>"4hXTCk……tAnaAT"</td><td>Fully signed transactions, compatible with encoding protocal base 64 and base 58, with base 64 being recommended</td></tr><tr><td>mode</td><td>Optional</td><td>"fast"<br>"sandwichMitigation"</td><td>BlockRazor offers two modes: Fast and SandwichMitigation, with Fast as the default.<br><br>In fast mode, transactions are sent based on globally distributed high-performance network and high-quality SWQoS, reaching the Leader node with the lowest latency.<br><br>In sandwichMitigation mode, transactions will be sent to BlockRazor's highly trusted SWQoS to reduce the attack surface. At the same time, transactions will skip the slot of the blacklisted Leader (dynamically identified by the BlockRazor sandwich monitoring mechanism), effectively reducing the risk of transactions being attacked by malicious Leaders.</td></tr><tr><td>safeWindow</td><td>Optional</td><td>3</td><td>safeWindow is used to determine the timing of transaction sending in sandwichMitigation mode and represents the number of consecutive slots of  whitelist validators. For example, if it is set to 3, the transaction will only be sent when 3 consecutive slots from the current slot belong to whitelist validators.<br><br>The range of safeWindow is 3-13. The larger the number, the better the effect of mitigating the sandwich attack, but it may have a certain impact on the rate of inclusion. If not set, the default is 3.</td></tr><tr><td>revertProtection</td><td>Optional</td><td>false</td><td>The default value is false. If set to true, the transaction will not fail on chain, but the speed of inclusion will be affected and there is a possibility that it cannot be included. Please choose to enable it carefully according to actual needs.</td></tr></tbody></table>





## **Priority** Fee <a href="#priority-fee-and-tip" id="priority-fee-and-tip"></a>

Priority Fee is an additional transaction fee charged by Solana on top of Base Fee (the minimum cost of sending a transaction, 5,000 lamports for each signature included in the transaction). Due to limited computing resources, Leader nodes order transactions mainly by transaction value when producing blocks. Transactions with higher Priority Fee have a higher probability of being included in the next block. The CU Price of Priority Fee is provided by [`getTransactionfee`](../../../../streams/network-fee-stream/solana/get-transactionfee.md) and is recommended to be set at least 1,000,000 when conscructing transactions.



## Tip <a href="#priority-fee-and-tip" id="priority-fee-and-tip"></a>

When constructing a transaction, you need to add a instruction of Tip transfer into the transaction(preferably added at the front position) to further speed up the inclusion. BlockRazor does not charge service fees from Tips. The Tip transfer amount is at least 1,000,000 Lamports (0.001 Sol) . It is recommended to set it to the value returned by [`getTransactionfee`](../../../../streams/network-fee-stream/solana/get-transactionfee.md). The account to receive Tip is:

```
"FjmZZrFvhnqqb9ThCuMVnENaM3JGVuGWNyCAxRJcFpg9",
"6No2i3aawzHsjtThw81iq1EXPJN6rh8eSJCLaYZfKDTG",
"A9cWowVAiHe9pJfKAj3TJiN9VpbzMUq6E4kEvf5mUT22",
"Gywj98ophM7GmkDdaWs4isqZnDdFCW7B46TXmKfvyqSm",
"68Pwb4jS7eZATjDfhmTXgRJjCiZmw1L7Huy4HNpnxJ3o",
"4ABhJh5rZPjv63RBJBuyWzBK3g9gWMUQdTZP2kiW31V9",
"B2M4NG5eyZp5SBQrSdtemzk5TqVuaWGQnowGaCBt8GyM",
"5jA59cXMKQqZAVdtopv8q3yyw9SYfiE3vUCbt7p8MfVf",
"5YktoWygr1Bp9wiS1xtMtUki1PeYuuzuCF98tqwYxf61",
"295Avbam4qGShBYK7E9H5Ldew4B3WyJGmgmXfiWdeeyV",
"EDi4rSy2LZgKJX74mbLTFk4mxoTgT6F7HxxzG2HBAFyK",
"BnGKHAC386n4Qmv9xtpBVbRaUTKixjBe3oagkPFKtoy6",
"Dd7K2Fp7AtoN8xCghKDRmyqr5U169t48Tw5fEd3wT9mq",
"AP6qExwrbRgBAVaehg4b5xHENX815sMabtBzUzVB4v8S",
```

{% hint style="info" %}
To avoid the degradation of performance due to address occupation, causing transaction delay, please rotate the Tip account when sending transactions.
{% endhint %}



