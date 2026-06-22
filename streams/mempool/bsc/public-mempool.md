# Public Mempool

### What is BSC Public Mempool

Public Mempool is a high-performance pending transaction stream based on [BEF](../../../core-technology/blockchain-edge-fabric.md), used for low-latency subscription to unconfirmed transactions in public propagation.

In the EVM network, transactions typically propagate through the mempool before entering a block. The core value of the Public Mempool is to help users obtain publicly available pending transaction signals earlier and integrate these signals into their strategy systems with lower latency. It is commonly used to monitor public trading activity, track Smart Money behavior, identify new opportunities, and provide faster signal input for strategies such as backrun, copy trading, and sniping. For systems that rely on pending signals to drive trading decisions, seeing transactions earlier often means:

* Entering the strategy judgment process earlier
* More time to complete calculations and risk control
* Higher probability of obtaining a better execution position in competitive scenarios

### Scenarios of BSC Public Mempool

* Pending Transaction Monitoring: Real-time monitoring of publicly distributed pending transactions to identify active addresses, popular contracts, or unusual transaction behavior.
* Smart Money Tracking: Track transaction activity at target addresses early on, providing signals for copy trading or strategy following.
* Backrun Discovery: Identifying publicly trades that may trigger backrun opportunities, allowing more time for subsequent strategy evaluation and trade submission.
* Sniping Opportunities: Capture the first signals in the open market as early as possible when new pools launch, liquidity injections occur, or target trades emerge.
* Real-time data input for strategies: Serving as a real-time input source for the trading system, it can be used in conjunction with capabilities such as Block Stream, Node Stream, RPC, or Block Builder to build a more complete monitoring and execution project.

### Benchmark

In our transaction reception latency benchmark, we compared BlockRazor with a regular Node in four regions: Dublin, Frankfurt, Tokyo, and Virginia. The evaluation was based on the time difference for clients receiving the same transaction from BlockRazor and regular Node among comparable samples.

<table><thead><tr><th width="134.609375">Region</th><th>BlockRazor Lead Rate</th><th>Avg Lead</th><th>P90 Lead</th></tr></thead><tbody><tr><td>Dublin</td><td>84.0%</td><td>102.4 ms</td><td>221.0 ms</td></tr><tr><td>Frankfurt</td><td>99.7%</td><td>30.4 ms</td><td>67.7 ms</td></tr><tr><td>Tokyo</td><td>99.9%</td><td>148.6 ms</td><td>264.4 ms</td></tr><tr><td>Virginia</td><td>99.7%</td><td>62.0 ms</td><td>190.7 ms</td></tr></tbody></table>

The results show that BlockRazor maintained a significant lead in all four regions. Its transaction reception lead rate exceeded 99% in Frankfurt, Tokyo, and Virginia, while its lead rate in Dublin was 84.0%. In terms of lead magnitude, BlockRazor's average lead time in different regions was approximately 102.4ms, 30.4ms, 148.6ms, and 62.0ms; under the P90 dimension, the lead magnitudes reached 221.0ms, 67.7ms, 264.4ms, and 190.7ms, respectively.

The results above demonstrate that BlockRazor exhibits a stable priority reception capability in the transaction propagation chain, enabling it to capture transactions earlier than ordinary nodes in the vast majority of comparable samples.

### Endpoint

<table><thead><tr><th width="160">Region</th><th>Availability Zone(AWS)</th><th>Relay Address</th></tr></thead><tbody><tr><td>Frankfurt</td><td>euc1-az2</td><td>35.157.64.49:50051</td></tr><tr><td>Tokyo</td><td>apne1-az4</td><td>54.249.93.63:50051</td></tr><tr><td>Ireland</td><td>euw1-az1</td><td>3.248.65.151:50051</td></tr><tr><td>Virginia</td><td>use1-az4</td><td>52.205.173.134:50051</td></tr></tbody></table>

### Rate Limit

The price is $300 per data stream per month. Please go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase.

{% hint style="info" %}
The number of data streams that can be subscribed to is calculated on a shared basis across all regions. For example, if you purchase one stream, you can only subscribe in one region; you will not be able to subscribe in other regions.
{% endhint %}

### Request Parameters

<table><thead><tr><th width="168">Parameters</th><th width="119">Mandatory</th><th width="103">Format</th><th width="98">Example</th><th>Description</th></tr></thead><tbody><tr><td>NodeValidation</td><td>Mandatory</td><td>boolean</td><td>false</td><td>This field currently only supports being set to <code>false</code>, and the relay will push all new transactions (unchecked) with lower latency.</td></tr></tbody></table>

### Request Example

[https://github.com/BlockRazorinc/relay\_example](https://github.com/BlockRazorinc/relay_example)

{% tabs %}
{% tab title="Go" %}
```go
package main

import (
	"context"
	"fmt"

	// directory of the generated code using the provided relay.proto file
	pb "github.com/BlockRazorinc/relay_example/protobuf"
	"github.com/ethereum/go-ethereum/core/types"
	"github.com/ethereum/go-ethereum/rlp"
	"google.golang.org/grpc"
)

// auth will be used to verify the credential
type Authentication struct {
	apiKey string
}

func (a *Authentication) GetRequestMetadata(context.Context, ...string) (map[string]string, error) {
	return map[string]string{"apiKey": a.apiKey}, nil
}

func (a *Authentication) RequireTransportSecurity() bool {
	return false
}

func main() {

	// BlockRazor relay endpoint address
	blzrelayEndPoint := "ip:port"

	// auth will be used to verify the credential
	auth := Authentication{
		"your auth token",
	}

	// open gRPC connection to BlockRazor relay
	var err error
	conn, err := grpc.Dial(blzrelayEndPoint, grpc.WithInsecure(), grpc.WithPerRPCCredentials(&auth), grpc.WithWriteBufferSize(0), grpc.WithInitialConnWindowSize(128*1024))
	if err != nil {
		fmt.Println("error: ", err)
		return
	}

	// use the Gateway client connection interface
	client := pb.NewGatewayClient(conn)

	// create context and defer cancel of context
	ctx, cancel := context.WithCancel(context.Background())
	defer cancel()

	// create a subscription using the stream-specific method and request
	stream, err := client.NewTxs(ctx, &pb.TxsRequest{NodeValidation: false})
	if err != nil {
		fmt.Println("failed to subscribe new tx: ", err)
		return
	}

	for {
		reply, err := stream.Recv()
		if err != nil {
			fmt.Println("stream receive error: ", err)
		}
		tx := &types.Transaction{}

		err = rlp.DecodeBytes(reply.Tx.RawTx, tx)
		if err != nil {
			continue
		}

		fmt.Println("recieve new tx, tx hash is ", tx.Hash().String())

	}
}
```
{% endtab %}
{% endtabs %}

#### Proto

The code of `relay.proto` is as follows:

```
syntax = "proto3";

package blockchain;

option go_package = "/Users/code/relay/grpcServer"; 
service Gateway {
  rpc SendTx (SendTxRequest) returns (SendTxReply) {}
  rpc SendTxs (SendTxsRequest) returns (SendTxsReply) {}
  rpc NewTxs (TxsRequest) returns (stream TxsReply){}
  rpc NewBlocks (BlocksRequest) returns (stream BlocksReply){}
}

message TxsRequest{
  bool node_validation = 1;
}

message Tx{
  bytes from = 1;
  int64 timestamp = 2;
  bytes raw_tx = 3;
}

message TxsReply{
   Tx tx = 1;
}

message BlocksRequest{
  bool node_validation = 1;
}

message BlockHeader{
  string parent_hash = 1;
  string sha3_uncles = 2;
  string miner = 3;
  string state_root = 4;
  string transactions_root = 5;
  string receipts_root = 6;
  string logs_bloom = 7;
  string difficulty = 8;
  string number = 9;
  uint64 gas_limit = 10;
  uint64 gas_used = 11;
  uint64 timestamp = 12;
  bytes extra_data = 13;
  string mix_hash = 14;
  uint64 nonce = 15;
  uint64 base_fee_per_gas = 16;
  string withdrawals_root = 17;
  uint64 blob_gas_used = 18;
  uint64 excess_blob_gas = 19;
  string parent_beacon_block_root = 20;
}

message NextValidator{
  string block_height = 1;
  string coinbase = 2;
}

message BlocksReply{
  string hash = 1;
  BlockHeader header = 2;
  repeated NextValidator nextValidator = 3;
  repeated Tx txs = 4;
}

message Transaction {
  string content = 1;
}

message Transactions {
  repeated Transaction transactions = 1;
}

message SendTxRequest {
  string transaction = 1;
}

message SendTxsRequest {
  string transactions = 1;
}

message SendTxReply {
  string tx_hash = 1;
}

message SendTxsReply {
  repeated string tx_hashs = 1;
}
```

### Response Example

**Success**

```json
{
  "tx":[
     {
        "raw_tx":"+QH0gjOthDuaygCDBrbAlKoP7P6dEOH8IzwtDAw9whDVeHKRhwFrzEHpAAC5AYTVQ9H9AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAmsrt4HBPm7jWohanh7XmbX9S/gRLrth87fXF3H2gC0FAAAAAAAAAAAAAAAAbsa1rd5IJ6lr43ixr1+LWmT/OhgAAAAAAAAAAAAAAABV05gyb5kFn/d1SFJGmZAnsxl5VQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABVkLNFR0SQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAGZ7qkBM09jlPtkQprbOV2bITVAfdbvzTltwBYjUJu6OIzF3aAAAAAAAAAAAAAAAAHqXLqcmW4qO1ZEAZXn2nYI/dKV1AAAAAAAAAAAAAAAAVdOYMm+ZBZ/3dUhSRpmQJ7MZeVUAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAASvCnY7scAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABme6pAgZOgy2LsKlIqPeeM7d520T3eAwIVk9O+vY4wT+zifYp0GGOgTY7Z5J3zs/YCj1HvVXOZF9Q2rj5x421GBG9CrKmxVGo="
     }
   ]
}
```

**Error**

```
rpc error: code = Unknown desc = data streams have exceeded its max limit [5]
```

