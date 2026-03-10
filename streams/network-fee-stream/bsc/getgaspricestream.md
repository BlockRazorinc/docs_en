# GetGasPriceStream

## Introduction

`GetGasPriceStream` provides gas price subscription service on BSC. It pushes the gas price of BSC transactions in recent block to users at a specified percentile based on gRPC stream. The endpoint is: <mark style="color:$primary;">grpc.bsc-fee.blockrazor.me:443</mark>



## Rate Limit

|         | Tier 4 | Tier 3 | Tier 2 | Tier 1 | Tier 0 |
| ------- | ------ | ------ | ------ | ------ | ------ |
| Streams | -      | -      | -      | -      | 10     |



## Request Parameter

<table><thead><tr><th width="131.4765625">Parameters</th><th width="131.76171875">Mandatory</th><th width="86.74609375">Format</th><th width="104.44140625">Example</th><th>Remarks</th></tr></thead><tbody><tr><td>percentile</td><td>mandatory</td><td>int</td><td>50</td><td>Get the gas price of the specified percentile, enumerated value: 25, 50, 75, 95, 99</td></tr><tr><td>blockRange</td><td>mandatory</td><td>int</td><td>20</td><td>Statistics of gas prices of transactions in the last N blocks, where N ranges from 1 to 20</td></tr></tbody></table>



## Request Example

```go
package main

import (
	"context"
	"crypto/tls"
	"log"

	// directory of the generated code using the provided proto file
	pb "fee-test/bscfeepb"

	"google.golang.org/grpc"
	"google.golang.org/grpc/credentials"
)

const (
	gRPCEndpoint = "grpc.bsc-fee.blockrazor.xyz:443" // endpoint address
	auth         = "your_auth" // auth to be verified
)

func main() {
	// open gRPC connection to endpoint
	conn, err := grpc.Dial(
		gRPCEndpoint,
		grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
		grpc.WithPerRPCCredentials(&Authentication{auth}),
	)
	if err != nil {
		panic(err)
	}
	defer conn.Close()
	
	// create the gRPC client
	client := pb.NewServerClient(conn)

	// send gRPC request
	req := &pb.TransactionFee{
		Percentile: 95,
		BlockRange: 10,
	}
	stream, err := client.GetGasPriceStream(context.Background(), req)
	if err != nil {
		panic(err)
	}

	for {
		message, err := stream.Recv()
		if err != nil {
			log.Printf("Failed to receive message: %v", err)
			break
		}
		log.Printf("Received message: %s\n", message.Time.AsTime().Format("2006-01-02 15:04:05"))
		log.Printf("Received GasPrice: %v\n", message.GasPrice.Percentile)
		log.Printf("Received GasPrice: %v\n", message.GasPrice.Value)
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
```



## Response Example

```json
2025/03/26 10:25:42 Received message: 2025-03-26 02:25:42
2025/03/26 10:25:42 Received GasPrice: 95
2025/03/26 10:25:42 Received GasPrice: 1000000000 // The gas price corresponding to the quantile, in wei
2025/03/26 10:25:45 Received message: 2025-03-26 02:25:45
2025/03/26 10:25:45 Received GasPrice: 95
2025/03/26 10:25:45 Received GasPrice: 1000000000
```



