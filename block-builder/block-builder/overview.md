# Overview

## Introduction

BlockRazor Builder constructs block with a high winning rate, due to its establishment of low-latency communication with Validators based on global deployment and multiple block construction algorithms to maximize block value. Currently bundle submission, private transaction submission and bundle simulation is supported.&#x20;

BlockRazor's Block Builder has a historical cumulative block production rate of 37%, ranking first in the entire BSC chain. To view the real-time block production rate, please visit [https://dune.com/bnbchain/bnb-smart-chain-mev-stats](https://dune.com/bnbchain/bnb-smart-chain-mev-stats).



## RPC Endpoint

| Globally applicable                                                |
| ------------------------------------------------------------------ |
| [https://rpc.blockrazor.builders](https://rpc.blockrazor.builders) |

This endpoint supports low-latency requests from users worldwide and is recommended for priority access.



<table><thead><tr><th width="136">Region</th><th width="219">Availability Zone(AWS)</th><th>RPC Endpoint</th></tr></thead><tbody><tr><td>Tokyo</td><td>apne1-az4</td><td><a href="https://tokyo.builder.blockrazor.io">https://tokyo.builder.blockrazor.io<br></a></td></tr><tr><td>Frankfurt</td><td>euc1-az2</td><td><a href="https://frankfurt.builder.blockrazor.io">https://frankfurt.builder.blockrazor.io<br></a></td></tr><tr><td>Virginia</td><td>use1-az4</td><td><a href="https://virginia.builder.blockrazor.io">https://virginia.builder.blockrazor.io<br></a></td></tr><tr><td>Dublin</td><td>euw1-az1</td><td><a href="https://dublin.builder.blockrazor.io">https://dublin.builder.blockrazor.io</a></td></tr></tbody></table>

To further achieve the lowest request latency, BlockRazor provides region-specific RPC endpoints. It is recommended to deploy the Bot in the Builder's region and complete the connection on the basis of having connected to the globally applicable endpoint.
