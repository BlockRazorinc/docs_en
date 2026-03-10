---
hidden: true
---

# Sandwich Detector

## Introduction

Sandwich Detector provides projects(e.g. wallet, DEX, and trading bot) with a sandwich attack monitoring service for BSC transactions. Projects can subscribe to the sandwich attack transaction information on BSC in real time based on gRPC. The subscription endpoint is: bsc.sandwich-detector.blockrazor.me:443



## Plan

|                   | Tier 4 | Tier 3 | Tier 2 | Tier 1 | Tier 0 |
| ----------------- | ------ | ------ | ------ | ------ | ------ |
| Sandwich Detector | -      | -      | -      | -      | ✅      |

The Sandwich Detector service will open a whitelist to projects(e.g. wallet, DEX, and trading bot)  subscribing to Tier 0 plan, who can monitor the sandwich attack information on BSC in real time. Please contact us after subscribing to the Tier 0 plan.



## Request Parameter

<table><thead><tr><th width="104.56640625">Parameters</th><th width="108.34765625">Mandatory</th><th width="80.796875">Format</th><th width="175.6015625">Example</th><th>Remarks</th></tr></thead><tbody><tr><td>from</td><td>optional</td><td>String</td><td>""0x3879……42d82a"</td><td>Filtering sandwich transactions by the "from" of the attacked transaction</td></tr><tr><td>to</td><td>optional</td><td>String</td><td>"0xda77……7098a2"</td><td>Filter sandwich transactions by the contract address that the attacked transaction has interacted with</td></tr><tr><td>method</td><td>optional</td><td>String</td><td>"0xac9650d8"</td><td>Filter sandwich transaction by the method called by the attacked transaction</td></tr></tbody></table>



## Request Example

{% tabs %}
{% tab title="grpcurl" %}
```go
# without filter
grpcurl -plaintext=false -import-path /path/to/proto -proto bscstream.proto -d ''  bsc.sandwich-detector.blockrazor.me:443 bscstream.TxStreamService/SubscribeTxStream
# with filter
grpcurl -plaintext=false -import-path /path/to/proto -proto bscstream.proto -d '{"to":"0xaa..bb"}'  bsc.sandwich-detector.blockrazor.me:443 bscstream.TxStreamService/SubscribeTxStream
```
{% endtab %}

{% tab title="Go" %}
```python
package main

import (
	"context"
	"crypto/tls"
	"log"

	pb "bscstream/proto/bscstream"

	"google.golang.org/grpc"
	"google.golang.org/grpc/credentials"
)

func main() {
	for {
		conn, err := grpc.Dial(
			"bsc.sandwich-detector.blockrazor.me:443",
			grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
			grpc.WithContextDialer(func(ctx context.Context, addr string) (net.Conn, error) {
				d := net.Dialer{DualStack: false}
				return d.DialContext(ctx, "tcp4", addr)
			}),
		)
		if err != nil {
			log.Printf("Failed to connect: %v.\n", err)
			continue
		}

		client := pb.NewTxStreamServiceClient(conn)
		stream, err := client.SubscribeTxStream(context.Background(), &pb.TxFilter{
			// Empty for no filter
			From:   "",
			To:     "",
			Method: "",
		})
		if err != nil {
			conn.Close()
			continue
		}

		log.Println("Successfully subscribed to the stream.")

		for {
			resp, err := stream.Recv()
			if err != nil {
				log.Printf("Error receiving stream data: %v. Reconnecting...\n", err)
				conn.Close()
				break
			}

			log.Printf("+%v\n", resp)
		}
	}
}

```
{% endtab %}
{% endtabs %}

### **Proto**

```go
// bscstream.proto
syntax = "proto3";

package bscstream;

option go_package = "proto/bscstream";

service TxStreamService {
  rpc SubscribeTxStream(TxFilter) returns (stream TxStreamResponse);
}

message TxFilter {
  string from = 1;   // (optional) from of victim tx to filter
  string to = 2;     // (optional) to of victim tx to filter
  string method = 3; // (optional) method of victim tx fo filter
}

message TxStreamResponse {
  repeated string txs = 1;         // all sandwich tx hash
  string victimtx = 2;             // victim tx hash
  repeated string attackertxs = 3; // frontrun and backrun tx hash
  string from = 4;                 // from of victim hash
  string to = 5;                   // to of victim hash
  string method = 6;               // method of victim hash
  repeated string tokens = 7;      // sandwiched token
  uint64 block = 8;                // block number of txs

  bool heartbeat = 9;              // if this resp is heartbeat, to keep stream alive if no sandwich data available
}
```



## Response Example

```json
{
  "txs": [
    "0xee5b2cfb7a5120206450b7edf2ac824ea810442d982b71923240115ef906acfa",
    "0xb2c9048de1af5be6733b3ed3d1ea4ac74c3d7a9e6c58a9e07ebdac7b8708399b",
    "0x046455f9207b5209489cfada58bfe593acdca58d4a730210e552e56199bfcfe8"
  ],
  "victimtx": "0xb2c9048de1af5be6733b3ed3d1ea4ac74c3d7a9e6c58a9e07ebdac7b8708399b",
  "attackertxs": [
    "0xee5b2cfb7a5120206450b7edf2ac824ea810442d982b71923240115ef906acfa",
    "0x046455f9207b5209489cfada58bfe593acdca58d4a730210e552e56199bfcfe8"
  ],
  "from": "0x387965d0b2dfbebb24aa02e0a068d79a0b42d82a",
  "to": "0xda77c035e4d5a748b4ab6674327fa446f17098a2",
  "method": "0xac9650d8",
  "tokens": [
    "0xdd1b2aaf66a030315a821e7588cf691d73b64444",
    "0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c"
  ],
  "block": "47993864"
}
```





