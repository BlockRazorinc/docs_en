# Send Bundle

{% hint style="warning" %}
Solana's bundle sending service is not bound to the subscription plan, with rate limit default to 3 TPS. API key could be required from [Authentication](../../../../get-started/authentication.md). If you need to increase the TPS limit, please [contact](https://discord.com/invite/qqJuwRb8Nh) us and we will handle it as soon as possible.
{% endhint %}

`Send Bundle` is a bundle sending interface provided by BlockRazor for Solana, used to send signed transactions to the blockchain in bundle form with low latency.

A maximum of four transactions can be sent in a single bundle. These transactions are executed sequentially, and if any one transaction fails, the entire bundle will fail.

To enhance MEV protection, use any valid Solana public key starting with `jitodontfront` and `dontbund1e` in the instructions of the first transaction in the bundle. If the transaction is subjected to a frontrun attack, it will be rejected by the Jito/Harmonic block engine.

### Endpoint <a href="#xian-liu" id="xian-liu"></a>

{% tabs %}
{% tab title="HTTP" %}
<table data-search="false"><thead><tr><th width="114.8828125">Region</th><th>URL</th></tr></thead><tbody><tr><td>Frankfurt</td><td>http://frankfurt.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Frankfurt</td><td>http://frankfurt-allnodes.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Frankfurt</td><td>http://frankfurt-cherryservers.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>New York</td><td>http://newyork.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Tokyo</td><td>http://tokyo.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Amsterdam</td><td>http://amsterdam.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Amsterdam</td><td>http://amsterdam-cherryservers.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>London</td><td>http://london.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Toronto</td><td>http://toronto.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Singapore</td><td>http://singapore.solana.blockrazor.xyz:443/sendBundle</td></tr><tr><td>Los Angeles</td><td>http://losangeles.solana.blockrazor.xyz:443/sendBundle</td></tr></tbody></table>
{% endtab %}

{% tab title="gRPC" %}
<table data-search="false"><thead><tr><th width="134.9765625">Region</th><th>URL</th></tr></thead><tbody><tr><td>Frankfurt</td><td>frankfurt.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Frankfurt</td><td>frankfurt-allnodes.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Frankfurt</td><td>frankfurt-cherryservers.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>New York</td><td>newyork.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Tokyo</td><td>tokyo.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Amsterdam</td><td>amsterdam.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Amsterdam</td><td>amsterdam-cherryservers.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>London</td><td>london.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Toronto</td><td>toronto.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Singapore</td><td>singapore.solana-grpc.blockrazor.xyz:80</td></tr><tr><td>Los Angeles</td><td>losangeles.solana-grpc.blockrazor.xyz:80</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

### Transaction Construction Example <a href="#jiao-yi-gou-jian-dai-ma-shi-li" id="jiao-yi-gou-jian-dai-ma-shi-li"></a>

* [Curl](curl.md)
* [Go](go.md)
* [Rust](rust.md)
* [JS](js.md)

### Request Parameter

<table><thead><tr><th width="111.44921875">Parameters</th><th width="115.421875">Mandatory</th><th width="104.94140625">Format</th><th width="109.98046875">Example</th><th>Description</th></tr></thead><tbody><tr><td>transactions</td><td>Mandatory</td><td>string[]</td><td>["$base64_tx_1","$base64_tx_2","$base64_tx_3"]</td><td>Fully signed transactions, Base64 encoding protocal </td></tr></tbody></table>

### **Priority** Fee <a href="#priority-fee-and-tip" id="priority-fee-and-tip"></a>

Priority Fee is an additional transaction fee charged by Solana on top of Base Fee (the minimum cost of sending a transaction, 5,000 lamports for each signature included in the transaction). Due to limited computing resources, Leader nodes order transactions mainly by transaction value when producing blocks. Transactions with higher Priority Fee have a higher probability of being included in the next block. The CU Price of Priority Fee is provided by [`getTransactionfee`](../../../../streams/network-fee-stream/solana/get-transactionfee.md) and is recommended to be set at least 1,000,000 when conscructing transactions.

### Tip <a href="#priority-fee-and-tip" id="priority-fee-and-tip"></a>

When constructing a transaction, you need to add a instruction of Tip transfer into the transaction(preferably added at the front position) to further speed up the inclusion. BlockRazor does not charge service fees from Tips. The Tip transfer amount is at least 100,000 Lamports (0.0001 Sol) . It is recommended to set it to the value returned by [`getTransactionfee`](../../../../streams/network-fee-stream/solana/get-transactionfee.md). The account to receive Tip is:

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

### Keep Alive <a href="#gou-jian-jiao-yi" id="gou-jian-jiao-yi"></a>

Send post request to the health endpoint to keep connection alive, the request is as follows:

{% tabs %}
{% tab title="CURL" %}
```bash
curl -X POST 'http://frankfurt.solana.blockrazor.xyz:443/health' \
-H "Content-Type: application/json" \
-H "apikey: <auth_token>" \
-d ""
```
{% endtab %}
{% endtabs %}
