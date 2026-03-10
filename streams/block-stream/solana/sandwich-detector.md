---
hidden: true
---

# Sandwich Detector

## Introduction

Sandwich Detector provides projects(e.g. wallet, DEX, and trading bot) with a sandwich attack monitoring service for Solana transactions. Users can subscribe to the sandwich attack transaction information on Solana in real time based on gRPC. The endpoint is: solana.sandwich-detector.blockrazor.me:443



## Plan

|                   | Tier 4 | Tier 3 | Tier 2 | Tier 1 | Tier 0 |
| ----------------- | ------ | ------ | ------ | ------ | ------ |
| Sandwich Detector | -      | -      | -      | -      | ✅      |

The Sandwich Detector service will open a whitelist to projects(e.g. wallet, DEX, and trading bot) subscribing to Tier 0 plan, who can monitor the sandwich attack information on Solana in real time. Please [contact](https://discord.com/invite/qqJuwRb8Nh) us after subscribing to the Tier 0 plan.



## Request Parameters

<table><thead><tr><th width="167.1328125">Parameters</th><th width="108.34765625">Mandatory</th><th width="80.796875">Format</th><th>Example</th><th>Remarks</th></tr></thead><tbody><tr><td>signer</td><td>optional</td><td>String</td><td>"6yf14f……iwPZ3V"</td><td>Filtering sandwich transactions by the originator’s account address</td></tr><tr><td>relevantProgramId</td><td>optional</td><td>String</td><td>"CAMMCz……KgrWqK"</td><td>Filter sandwich transactions by the programId that the attacked transaction has been interacted with</td></tr></tbody></table>



## Request Example

{% tabs %}
{% tab title="grpcurl" %}
```go
# without filter
grpcurl -plaintext=false -import-path /path/to/proto -proto solstream.proto -d ''  solana.sandwich-detector.blockrazor.me:443 solstream.TxStreamService/SubscribeTxStream
# with filter
grpcurl -plaintext=false -import-path /path/to/proto -proto solstream.proto -d '{"relevantProgramId":"aa..bb"}'  solana.sandwich-detector.blockrazor.me:443 solstream.TxStreamService/SubscribeTxStream
```
{% endtab %}

{% tab title="Go" %}
```python
package main

import (
	"context"
	"crypto/tls"
	"log"

	pb "solstream/proto/solstream"

	"google.golang.org/grpc"
	"google.golang.org/grpc/credentials"
)

func main() {
	for {
		conn, err := grpc.Dial(
			"solana.sandwich-detector.blockrazor.me:443",
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
			Signer:            "",
			RelevantProgramId: "",
		})
		if err != nil {
			log.Printf("Error subscribing to stream: %v.\n", err)
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
			log.Println(resp)

		}
	}

}
```
{% endtab %}
{% endtabs %}

### **Proto**

```go
// solstream.proto
syntax = "proto3";

package solstream;

option go_package = "proto/solstream";

service TxStreamService {
  rpc SubscribeTxStream(TxFilter) returns (stream TxStreamResponse);
}

message TxFilter {
  string signer = 1;            // (optional) signer of victim tx to filter
  string relevantProgramId = 2; // (optional) interacted program id of victim tx to filter. For example, programId of some router
}

message TxStreamResponse {
  uint64 slot = 1;                 // slot of sandwich txs
  repeated string txs = 2;         // all sandwich tx signatures
  string victimtx = 3;             // victim tx signature
  repeated string attackertxs = 4; // frontrun and backrun tx signature
  string signer = 5;               // signaer of victim tx

  bool heartbeat = 6;              // if this resp is heartbeat, to keep stream alive if no sandwich data available
}
```



## Response Example

```json
{
  "slot": "330748316",
  "txs": [
    "3gDiqwyYnqLtBrkdF5Y6RJiattctYjKu2NfjcAupDBRkhodh9a22XjPYYdhf83FpGUnBe2g1oeLxfpNYG8QyCrUt",
    "4joomCxakJxi9vhJ6mRuFStyiUyetaB2X1HMj4g3VUSTMQkPgMTAZ7NaLNMejvfu9zdp7gXp2fM5UEgVK5PohVrP",
    "4QgGbPiaNyhgMrkeFrNjZaPNDQTvXqc1THVQJXvbN26gBt8GxQikBzk5fiQyjvffLt8PJUGNw21GU55iErmQcGkC"
  ],
  "victimtx": "4joomCxakJxi9vhJ6mRuFStyiUyetaB2X1HMj4g3VUSTMQkPgMTAZ7NaLNMejvfu9zdp7gXp2fM5UEgVK5PohVrP",
  "attackertxs": [
    "3gDiqwyYnqLtBrkdF5Y6RJiattctYjKu2NfjcAupDBRkhodh9a22XjPYYdhf83FpGUnBe2g1oeLxfpNYG8QyCrUt",
    "4QgGbPiaNyhgMrkeFrNjZaPNDQTvXqc1THVQJXvbN26gBt8GxQikBzk5fiQyjvffLt8PJUGNw21GU55iErmQcGkC"
  ],
  "signer": "Ejhath43fHYtWLbSMfVHCL8eJiLkV22K6w1Ni5xzXofX" // signer of victim tx
}
```





