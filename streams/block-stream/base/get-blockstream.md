# Get BlockStream

## Introduction

This method is used to retrieve block data from Base and supports the gRPC protocol.



## Endpoint

{% tabs %}
{% tab title="gRPC" %}
<table><thead><tr><th width="138.33984375">Region</th><th>Endpoint</th></tr></thead><tbody><tr><td>Frankfurt</td><td>frankfurt.grpc.base.blockrazor.xyz:80</td></tr><tr><td>Virginia</td><td>virginia.grpc.base.blockrazor.xyz:80</td></tr><tr><td>Tokyo</td><td>tokyo.grpc.base.blockrazor.xyz:80</td></tr></tbody></table>
{% endtab %}
{% endtabs %}



## Rate Limit

|             | Tier 4 | Tier 3 | Tier 2 | Tier 1 | Tier 0 |
| ----------- | ------ | ------ | ------ | ------ | ------ |
| BlockStream | -      | -      | -      | ✅      | ✅      |



## Request Example

{% tabs %}
{% tab title="gRPC" %}
Access the example [here](https://github.com/BlockRazorinc/base-api-client-go/blob/c4bec3d65e55ffb0da07253fa78aefe1b1c07e33/main.go#L42)

```go
// GetBlockStream provides a simplified example of subscribing to and processing the regular block stream.
// Note: This function attempts to connect and subscribe only once. For production use, implement your own reconnection logic.
func GetBlockStream(authToken string) {
	log.Printf("[BlockStream] Attempting to connect to gRPC server at %s...", grpcAddr)

	// Establish a connection to the gRPC server with a timeout.
	ctx, cancel := context.WithTimeout(context.Background(), 30*time.Second)
	defer cancel()
	conn, err := grpc.DialContext(ctx, grpcAddr,
		grpc.WithTransportCredentials(insecure.NewCredentials()))
	if err != nil {
		log.Printf("[BlockStream] Failed to connect to gRPC server: %v", err)
		return
	}
	defer conn.Close()

	log.Println("[BlockStream] Successfully connected to gRPC server.")
	client := basepb.NewBaseApiClient(conn)

	// Create a new context with authentication metadata for the stream subscription.
	streamCtx := metadata.NewOutgoingContext(context.Background(), metadata.Pairs("authorization", authToken))
	stream, err := client.GetBlockStream(streamCtx, &basepb.GetBlockStreamRequest{})
	if err != nil {
		log.Printf("[BlockStream] Failed to subscribe to stream: %v", err)
		return
	}

	log.Println("[BlockStream] Subscription successful. Waiting for new blocks...")

	// Loop indefinitely to receive messages from the stream.
	for {
		block, err := stream.Recv()
		if err != nil {
			if err == io.EOF {
				log.Println("[BlockStream] Stream closed by the server (EOF).")
			} else {
				log.Printf("[BlockStream] An error occurred while receiving data: %v", err)
			}
			break // Exit the loop on error or stream closure.
		}

		// Process the received block data.
		log.Printf("=> [BlockStream] Received new block: Number=%d, Hash=%s, TransactionCount=%d",
			block.GetBlockNumber(),
			block.GetBlockHash(),
			len(block.GetTransactions()),
		)
		// To decode transactions, you can call DecodeTransactions(block.Transactions).
	}
}
```
{% endtab %}
{% endtabs %}

#### [proto](https://github.com/BlockRazorinc/base-api-client-go/blob/1d46c2983420d6da645992a9f3ed51688f7dac88/proto/BaseApi.proto)

```go
syntax = "proto3";

option go_package = "./basepb";


import "google/protobuf/wrappers.proto";

message BaseBlock {
  string parent_hash = 1;
  string fee_recipient = 2;
  bytes state_root = 3;
  bytes receipts_root = 4;
  bytes logs_bloom = 5;
  bytes prev_randao = 6;
  uint64 block_number = 7;
  uint64 gas_limit = 8;
  uint64 gas_used = 9;
  uint64 timestamp = 10;
  bytes extra_data = 11;
  repeated uint64 base_fee_per_gas = 12;
  string block_hash = 13;
  repeated bytes transactions = 14;

  repeated Withdrawal withdrawals = 15;
  google.protobuf.UInt64Value blob_gas_used = 16;
  google.protobuf.UInt64Value excess_blob_gas = 17;
  google.protobuf.BytesValue withdrawals_root = 18;
}

message Withdrawal {
  uint64 index = 1;
  uint64 validator = 2;
  bytes address = 3;
  uint64 amount = 4;
}

message GetRawFlashBlocksStreamRequest {
}

message GetBlockStreamRequest {
}

message SendTransactionRequest {
  string rawTransaction = 1;
}

message SendTransactionResponse {
  string txHash = 1;
}

message FlashBlockStrRequest {
}

message RawFlashBlockStrResponse {
  bytes message = 1;
}

service BaseApi {
  rpc SendTransaction(SendTransactionRequest) returns (SendTransactionResponse);
  rpc GetBlockStream(GetBlockStreamRequest) returns (stream BaseBlock);
  rpc GetRawFlashBlockStream(GetRawFlashBlocksStreamRequest) returns (stream RawFlashBlockStrResponse);
}
```



## Response

**Normal**

```go
Number=35347872, Hash=0x1c1dd5911cf8fe47c227159f5e3dad08d289879a225b6d51840f4ecd0b212dd8, TransactionCount=252
```



**Abnormal**

```go
rpc error: code = Unknown desc = Authentication information is missing. Please provide a valid auth token
```



