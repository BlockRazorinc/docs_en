---
description: >-
  Introduction to eth_sendRawTransaction v2 of BlockRazor BSC Fast mode and
  integration methods
hidden: true
---

# eth\_sendRawTransaction v2

### Introduction <a href="#jie-shao" id="jie-shao"></a>

Compared with [eth\_sendRawTransaction](eth_sendrawtransaction.md), `eth_sendRawTransaction v2` presents a much more streamlined and rapid method for submitting transactions.

* Bypasses CORS Preflight: It eliminates the delay (50-100ms) that is typically incurred by OPTIONS preflight.
* Plain Text over JSON: Employing a simple plain text transmission circumvents the computational burden associated with parsing JSON. Furthermore, the resulting smaller data size serves to cut down on network transfer time and costs.

The features of `eth_sendRawTransaction v2` are more suitable for front-end transaction application projects with a global user base.

{% hint style="info" %}
Fast Mode is not tied to the subscription plan, but each transaction sent in Fast Mode must include a tip sent to the address `0x9D70AC39166ca154307a93fa6b595CF7962fe8e5`. The minimum tip amount is the greater of 0.000025 BNB or Transaction Fee \* 5%.
{% endhint %}

### Endpoint <a href="#xian-liu" id="xian-liu"></a>

{% tabs %}
{% tab title="General" %}
```
http://bsc-fast.blockrazor.io/v2/sendRawTransaction
```
{% endtab %}

{% tab title="Geographic" %}
<table><thead><tr><th width="117.94140625">Region</th><th>Domain</th></tr></thead><tbody><tr><td>Frankfurt</td><td>http://frankfurt.bsc-fast.blockrazor.io/v2/sendRawTransaction</td></tr><tr><td>Japan</td><td>http://japan.bsc-fast.blockrazor.io/v2/sendRawTransaction</td></tr><tr><td>Virginia</td><td>http://virginia.bsc-fast.blockrazor.io/v2/sendRawTransaction</td></tr></tbody></table>
{% endtab %}
{% endtabs %}

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

### Keep Alive <a href="#keep-alive" id="keep-alive"></a>

Please send a POST request to the health check endpoint to keep the connection alive. We recommend sending a request every 10 seconds. Below is a request example:

{% tabs %}
{% tab title="Curl" %}
```json
curl -X POST 'http://bsc-fast.blockrazor.io/health' \
-H "Content-Type: text/plain" \
-d ""
```
{% endtab %}
{% endtabs %}
