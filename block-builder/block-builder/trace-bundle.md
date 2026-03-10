# Trace Bundle

### Introduction

This method supports querying the current status of the bundle by bundle hash. Please query 5 minutes after sending the bundle to the builder. Endpoint: [https://bsc-bundle-stats.blockrazor.io/](https://bsc-bundle-stats.blockrazor.io/)



### Rate Limit

<table><thead><tr><th width="165.7890625"></th><th>Tier 4</th><th>Tier 3</th><th>Tier 2</th><th>Tier 1</th><th>Tier 0</th></tr></thead><tbody><tr><td>txs limit / day </td><td>4 / day</td><td>8 / day</td><td>40 / day</td><td>200 / day</td><td>Unlimited</td></tr></tbody></table>



### Request Parameter

<table><thead><tr><th width="156">Parameters</th><th width="124">Mandatory</th><th width="122">Format</th><th>Example</th><th>Description</th></tr></thead><tbody><tr><td>hash</td><td>Mandatory</td><td>hash</td><td>0x25f9……317097</td><td>bundle hash</td></tr></tbody></table>



### Request Example

{% tabs %}
{% tab title="HTTPS" %}
```json
curl -X GET "https://bsc-bundle-stats.blockrazor.io/bundlestate?hash=0x25f9fc35e978709195c00e864b9a19fb41ad5c5c5b8a3e003813ae9727317097" \
     -H "Content-Type: application/json" \
     -H "Authorization: M2ZiZj……JhODA1"‍
```
{% endtab %}
{% endtabs %}



### Response Example

**Success**

```json
{
  "bundle": {
    "timestamp": "2025-04-07T09:04:40Z", // The time when the builder receives the bundle (UTC)
    "bundleHash": "0x25f9fc35e978709195c00e864b9a19fb41ad5c5c5b8a3e003813ae9727317097", // bundle hash
    "state": "onchain", // bundle is included on chain
    "blockNumber": 48144954, // The block number where the bundle is located
    "priority": "358911000000000" // bundle value, in wei
  }
}
```

**Error**

```json
{
  "bundle": {
    "timestamp": "2025-04-08T05:21:10Z", // The time when the builder receives the bundle (UTC)
    "bundleHash": "0xe06a923bce1f46b2a0602b8fb2263dffde22f21277b0b71d84b79aff6a58772b", // bundle hash
    "state": "failed", // builder has received bundle，but the bundle is not included
    "err": "non-reverting tx in bundle failed" // reason why the bundle is not included
  }
}
```

```json
{
  "bundle": {
    "bundleHash": "0xabc", // bundle hash in the request
    "state": "not found" // bundle is not found
  }
}
```

