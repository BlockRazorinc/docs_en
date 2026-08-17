---
description: >-
  Introduction to BlockRazor Base Transaction Sending mode and API integration
  documentation
---

# Base Transaction Sending

Base RPC is a transaction sending interface provided by BlockRazor for Base, used to send signed raw transactions. Currently, it only supports the `eth_sendRawTransaction` method and provides both gRPC and HTTPS.

### Why choose BlockRazor Base RPC?

For Wallets and DEXs, directly connecting to the official Base Sequencer can meet basic sending requirements, but for businesses serving global users and focusing on cross-regional performance and production environment stability, the sending path itself still has room for further optimization. For a detailed comparison of BlockRazor Base RPC and the official sending service, please refer to the [Benchmark](https://blockrazor.io/blog/20250922basebenchmark/).

**Global multi-point deployment**

Compared to directly connecting to the Base Sequencer, BlockRazor Base RPC provides sending entry points in multiple core regions, making it suitable for wallets and DEXs to choose the nearest endpoint based on their service deployment location. For businesses serving global users, sending entry points closer to business servers and core user regions typically help shorten request paths and improve transaction sending efficiency.

**Intercontinental express lines**

BlockRazor Base RPC's optimization focuses not only on ingress node deployment but also on data transmission links between regional relays. Compared to inter-regional forwarding methods that rely entirely on ordinary public network routing, intercontinental express lines can significantly reduce the impact of routing fluctuations, congestion, and link jitter in inter-relay transmission, improving the stability and consistency of transaction requests throughout the overall transmission routing.
