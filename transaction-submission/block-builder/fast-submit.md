---
description: Introduction to Fast Submit of BlockRazor Block Builder and access methods
---

# Fast Submit

### What is Fast Submit?

Fast Submit is a dedicated transaction submission channel provided by BlockRazor for BSC Block Builder. It optimizes the network path and request processing path of transactions from the client to the Builder, improving submission speed and stability.

In the BSC Builder scenario, transaction quality depends on more than just transaction content, gas, slippage, and timing of delivery. For latency-sensitive users, those deploying across regions, or those prioritizing stability, the path a transaction takes to reach the Builder is itself a part of the commit quality.

Fast Submit does not change the transaction logic, nor does it require users to rewrite the existing submission process. It optimizes the submission link between the client and the Builder, allowing transactions to reach the Builder faster and making the submission link more stable under high load and cross-region scenarios, reducing the additional overhead caused by intermediate forwarding, proxy processing, and public network fluctuations.

### Why is Fast Submit faster and more stable?

**Dedicated HTTP domain**

Transaction requests in the regular submission channel pass through the CloudFront proxy layer before reaching the Block Builder, incurring more intermediate forwarding, network hops, and additional TLS and proxy processing overhead. In scenarios with network congestion or high concurrency, the queuing, forwarding, and processing time caused by these additional steps is often amplified, making request latency and fluctuations more pronounced.

In contrast, Fast Submit supports submitting requests via a dedicated HTTP domain, removes the CloudFront proxy layer, compresses the submission path between the client and the Block Builder, and reduces the additional overhead caused by intermediate layers.

**Intercontinental express lines**

In cross-regional scenarios, regular submission channels rely on public network paths, making them susceptible to routing fluctuations, link congestion, and network jitter. Especially during intercontinental transmissions, these unstable factors amplify request latency and volatility, reducing the consistency of the submission link.

Fast Submit submits transactions to Block Builder via intercontinental dedicated network lines, minimizing the impact of public network instability on the request link and providing a more stable and lower latency submission experience.

### Benchmark

Benchmark shows that Fast Submit can significantly reduce submission path latency compared with the standard submission channel.&#x20;

On intercontinental routes, latency can be reduced by about 50 ms, which can improve the transaction’s 0-block inclusion rate by about 11% under BSC’s current block time of around 450 ms. If block time further decreases to 250 ms in the future, the improvement could increase to about 20%.&#x20;

On inland routes, latency can be reduced by about 20 ms, improving the transaction’s 0-block inclusion rate by about 4.4% under the current block time. If block time decreases to 250 ms in the future, the improvement could further increase to about 8%.

### What users is Fast Submit suitable for?

Fast Submit is more suitable for users who already have a mature submission process and have specific requirements for latency, stability, and cross-region performance.

* **Searcher**: MEV participants who focus on transaction submission timing, path quality, and cross-regional stability.
* **Trading Bot / Quant Team**: Team with specific requirements for execution speed, high-frequency submissions, and regional consistency.
* **Wallets / DEXs**: Team aiming to optimize the user transaction submission experience without altering the existing sending logic.

### Benchmark



### Access method

Developers simply need to switch their existing HTTP submission requests to the dedicated Fast Submit domain. The integration process is as follows:

1. Go to the Pricing page to purchase the package
2. Contact us to obtain your dedicated Fast Submit domain.
3. Keep the original request logic unchanged, and send the existing transaction submission request to this dedicated HTTP domain.
4. The submission latency and stability performance were evaluated by testing in actual deployment areas and compared with the original submission channel.

### Precautions

Fast Submit aims to optimize the speed and stability of transactions reaching the BSC Block Builder, but it does not guarantee that a transaction will be packaged. Fast Submit is an infrastructure optimization capability for the submission chain, not a promise of a inclusion result.

Whether a transaction is ultimately included in a block still depends on a variety of factors beyond the submission chain, including but not limited to: market competition, Builder processing strategy, current block space, transaction quality, and real-time on-chain congestion.
