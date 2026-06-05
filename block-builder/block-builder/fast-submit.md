# Fast Submit

### Introduction

Fast Submit is a dedicated transaction submission channel for BSC Block Builder, designed to improve the speed and stability of transaction submissions.

For latency-sensitive transactions, the speed and stability with which a transaction reaches the Block Builder directly impacts the submission outcome. Additional proxy layers, cross-regional network jitter, and extra overhead in the request processing chain can still introduce unnecessary transaction delays.

Compared to general public commit channels, Fast Submit focuses on optimizing the network path and request processing path between the client and the Builder. Its core goal is clear:

* Get transactions to Builder faster
* Make the submission process more stable under high load and cross-regional scenarios.
* Reduce avoidable overhead caused by additional proxies, network fluctuations, and duplicate processing.

### Why is Fast Submit faster and more stable?

**Dedicated HTTP domain**

Fast Submit provides a dedicated HTTP domain for transaction submission. By replacing the CloudFront proxy layer with direct DNS resolution, it reduces the additional network overhead caused by intermediate forwarding and TLS authentication. This means a more direct request path, fewer network hops, and lower latency and fluctuations.

**Intercontinental express lines**

Fast Submit uses intercontinental leased network lines to submit transactions to Block Builder, reducing the impact of unstable factors such as public network routing fluctuations, congestion, and jitter on transaction requests.

### Price

Fast Submit is only included in the Package. Please go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase the Package. After subscribing, please [contact](https://discord.com/invite/qqJuwRb8Nh) us to connect your dedicated domain name.

### Integration

Users could simply need to switch their existing HTTP submission requests to the dedicated Fast Submit domain. The integration process is as follows:

1. Go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase the package
2. [Contact](https://discord.com/invite/qqJuwRb8Nh) us to obtain your dedicated Fast Submit domain.
3. Keep the original request logic unchanged, and send the existing transaction submission request to this dedicated HTTP domain.
4. The submission latency and stability performance could be evaluated by testing in actual deployment areas and compared with the original submission channel.

### Precautions

Fast Submit aims to optimize the speed and stability of transactions reaching the BSC Block Builder, but it does not guarantee that a transaction will be included. Fast Submit is an infrastructure optimization capability for the submission chain, not a promise of inclusion.

Whether a transaction is ultimately included in a block still depends on a variety of factors beyond the submission chain, including but not limited to: market competition, Builder processing strategy, current block space, transaction quality, and real-time on-chain congestion.
