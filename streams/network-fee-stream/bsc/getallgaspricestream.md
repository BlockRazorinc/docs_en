# GetAllGasPriceStream

## Introduction

`GetAllGasPriceStream` provides gas price subscription service on BSC. It pushes the gas price of BSC transactions in recent block to users at all percentile based on gRPC stream. The endpoint is: <mark style="color:$primary;">grpc.bsc-fee.blockrazor.me:443</mark>



## Rate Limit

|         | Tier 4 | Tier 3 | Tier 2 | Tier 1 | Tier 0 |
| ------- | ------ | ------ | ------ | ------ | ------ |
| Streams | -      | -      | -      | -      | 10     |



## Request Parameter

<table><thead><tr><th width="131.4765625">Parameters</th><th width="131.76171875">Mandatory</th><th width="86.74609375">Format</th><th width="104.44140625">Example</th><th>Remarks</th></tr></thead><tbody><tr><td>blockRange</td><td>mandatory</td><td>int</td><td>20</td><td>Statistics of gas prices of transactions in the last N blocks, where N ranges from 1 to 20</td></tr></tbody></table>



## Request Example

```go
package main

import (
	"context"
	"crypto/tls"
	"log"

	pb "fee-test/bscfeepb"

	"google.golang.org/grpc"
	"google.golang.org/grpc/credentials"
)

const (
	gRPCEndpoint = "grpc.bsc-fee.blockrazor.xyz:443"
	auth         = "your_auth"
)

func main() {
	conn, err := grpc.Dial(
		gRPCEndpoint,
		grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
		grpc.WithPerRPCCredentials(&Authentication{auth}),
	)
	if err != nil {
		panic(err)
	}
	defer conn.Close()

	client := pb.NewServerClient(conn)

	req := &pb.BlockRange{
		BlockRange: 5,
	}
	stream, err := client.GetAllGasPriceStream(context.Background(), req)
	if err != nil {
		panic(err)
	}

	for {
		message, err := stream.Recv()
		if err != nil {
			log.Printf("Failed to receive message: %v", err)
			break
		}
		log.Printf("Received Time: %s\n", message.Time.AsTime().Format("2006-01-02 15:04:05"))
		for _, gasPrice := range message.AllGasPrice {
			log.Printf("Received message percentile: %d\n", gasPrice.Percentile)
			log.Printf("Received message value: %s\n", gasPrice.Value)
		}
	}
}

type Authentication struct {
	auth string
}

func (a *Authentication) GetRequestMetadata(context.Context, ...string) (map[string]string, error) {
	return map[string]string{"apiKey": a.auth}, nil
}

func (a *Authentication) RequireTransportSecurity() bool {
	return false
}
```



### Proto

```json
syntax = "proto3";

package bscfeepb;

import "google/protobuf/timestamp.proto";

option go_package = "./pb/bscfeepb";

service Server {
    rpc GetGasPriceStream(TransactionFee) returns(stream TransactionFeeStreamResponse) {};
    rpc GetAllGasPriceStream(BlockRange) returns(stream AllGasPriceStreamResponse) {};
}

message TransactionFee {
    int32 percentile = 1;
    int32 blockRange = 2;
}

message FeeValue {
    int32 percentile = 1;
    string value = 2;
}

message TransactionFeeStreamResponse {
    FeeValue gasPrice = 1;
    google.protobuf.Timestamp time = 2;
}

message BlockRange {
    int32 blockRange = 2;
}

message AllGasPriceStreamResponse {
    repeated FeeValue allGasPrice = 1;
    google.protobuf.Timestamp time = 2;
}
```



## Response Example

```json
2025/04/08 10:18:21 Received Time: 2025-04-08 02:18:21
2025/04/08 10:18:21 Received message percentile: 25
2025/04/08 10:18:21 Received message value: 1000000000 //// The gas price corresponding to the quantile, in wei
2025/04/08 10:18:21 Received message percentile: 50
2025/04/08 10:18:21 Received message value: 1100000000
2025/04/08 10:18:21 Received message percentile: 75
2025/04/08 10:18:21 Received message value: 2020000000
2025/04/08 10:18:21 Received message percentile: 95
2025/04/08 10:18:21 Received message value: 5000000000
2025/04/08 10:18:21 Received message percentile: 99
2025/04/08 10:18:21 Received message value: 20000000000
```



