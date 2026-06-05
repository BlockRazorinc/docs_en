# Tx Trace

### Introduction

Tx Trace is a tool for tracking the propagation of transactions, used to query the propagation path and time difference of a specified transaction across the global network. Built on BlockRazor's high-performance global network, it enhances the observability of transactions at the network propagation layer, helping users see when a transaction enters the network, which region it first enters, and how long it takes to propagate in each region. Tx Trace is applicable in the following scenarios:

* Transaction delay investigation
* Multi-region node deployment assessment
* High-frequency trading pipeline optimization
* private/public path validation

Compared to traditional RPC submission results, Tx Trace supplements the propagation process data. It cannot replace on-chain receipt queries, but it can provide an observation perspective closer to the network layer, helping users to transform transaction propagation analysis from black-box judgment to data analysis based on region and time difference.

Tx Trace queries are limited by a validity window and do not support querying the full historical transaction set.

### Price

| User Type            | Limit                | Price        |
| -------------------- | -------------------- | ------------ |
| New registered users | 20 requests per day  | Free         |
| Paid users           | 500 requests per day | $500 / month |

### Endpoint

http://tx-trace.blockrazor.io

### Request Example

```bash
curl -H "Authorization: <YOUR_AUTHORIZATION>" \
  http://tx-trace.blockrazor.io/txtrace/0xea4cac1749fcbfd53d798edf795d80c550aa00873d3acb1019000bf74dd18404
```

### Response Example

**Normal**

```json
{
	"txTrace": [{
		"region": "EU Germany",
		"txTime": "2026-06-03 03:18:10.481",
		"diff": "+0ms"
	},
	{
		"region": "NA US Virginia",
		"txTime": "2026-06-03 03:18:10.510",
		"diff": "+29ms" // The transaction spread from EU Germany to NA US Virginia in 29ms.
	},
	},
	{
		"region": "EU Ireland",
		"txTime": "2026-06-03 03:18:10.515",
		"diff": "+34ms" // The transaction spread from EU Germany to EU Ireland in 34ms.
	},
	{
		"region": "AS Japan",
		"txTime": "2026-06-03 03:18:10.574",
		"diff": "+93ms"
	}],
	"txHash": "0xe55b39c4dead92fe956f7ce2d640e0fcf0ce0cd969da9e3f900d493634b64a54",
	"numberOfRegions": 4
}
```

**Abnormal**

```json
{"error":"invalid token"}
```

```json
{"error":"daily limit exceeded"}
```
