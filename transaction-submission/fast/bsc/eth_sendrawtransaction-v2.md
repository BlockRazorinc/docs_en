# eth\_sendRawTransaction v2

### Introduction <a href="#jie-shao" id="jie-shao"></a>

The Fast Mode leverages BlockRazor's global high-performance network to achieve the lowest latency for transaction inclusion, making it suitable for users who have extreme requirements for transaction inclusion speed.&#x20;

Compared to [Send RawTx](send-rawtx.md),  `eth_sendRawTransaction` will not broadcasting txs via the mempool, ensuring both speed and privacy.

{% hint style="info" %}
Fast Mode is not tied to the subscription plan, but each transaction sent in Fast Mode must include a tip sent to the address `0x9D70AC39166ca154307a93fa6b595CF7962fe8e5`. The minimum tip amount is the greater of 0.000025 BNB or Transaction Fee \* 5%.
{% endhint %}

Compared with [eth\_sendRawTransaction](eth_sendrawtransaction.md), `eth_sendRawTransaction v2` presents a much more streamlined and rapid method for submitting transactions.

* Bypasses CORS Preflight: It eliminates the delay (50-100ms) that is typically incurred by OPTIONS preflight.
* Plain Text over JSON: Employing a simple plain text transmission circumvents the computational burden associated with parsing JSON. Furthermore, the resulting smaller data size serves to cut down on network transfer time and costs.



### Endpoint <a href="#xian-liu" id="xian-liu"></a>

http://bsc-fast.blockrazor.io/v2/sendRawTransaction



### Rate Limit <a href="#xian-liu" id="xian-liu"></a>

Fast Mode is not tied to the subscription plan, the rate limit default to 10 TPS for all users. Please contact us if you require an increase in your TPS limit.



### Request Example <a href="#jiao-yi-gou-jian-dai-ma-shi-li" id="jiao-yi-gou-jian-dai-ma-shi-li"></a>

{% tabs %}
{% tab title="CURL" %}
```javascript
curl -X POST 'http://bsc-fast.blockrazor.io/v2/sendRawTransaction?auth=<auth_token>' \
-H "Content-Type: text/plain" \
-d "<raw_tx>"
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**Note:**

* **the `auth` are compulsory to be added in URI params**
* **the only header permitted in the request is `Content-Type: text/plain`**
{% endhint %}



### Response

**Normal**

```json
{
	"code": 0,
	"message": "success",
	"data": {
		"txHash": "0xd2ebb523f400dd33ebf946a1280426196eed72c9a63b7e1734dd6f8e2f5a81dc"
	}
}
```

**Abnormal**

```json
{
	"code": -32600,
	"message": "auth token is invalid",
	"data": null
}
```
