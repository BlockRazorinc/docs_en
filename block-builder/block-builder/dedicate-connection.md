---
hidden: true
---

# Dedicate Connection

Dedicate Connection is a dedicated connection service designed for low-latency transaction submission scenarios. It supports deploying clients and servers in the same data center and exposes the Block Builder's `IP:port` for direct calls. Compared to submitting transactions via HTTP domain names, Dedicate Connection provides a more direct and lower-level Builder access method, minimizing the overhead of shared entry points, proxy layers, and additional encapsulation. This shortens the actual network path from the client to the Builder, thereby improving the stability, determinism, and controllability of the submission chain.

### Difference between Fast Submit and Dedicate Submission

Both Dedicate Connection and Fast Submit are used to improve the efficiency and stability of submitting transactions to BSC Block Builder, but they have different focuses. Fast Submit is an optimized standard access solution. Developers typically only need to use a dedicated HTTP domain name to obtain a faster and more stable submission experience through a more direct network path, optimized cross-region links, and optimized server request processing. It is suitable for scenarios that want to improve the quality of the submission link with lower access costs.

Dedicate Connection emphasizes the shortest path and link control, opens the Builder's IP:port, and supports the deployment of clients and servers in the same data center. It is suitable for teams that are extremely sensitive to latency, want to control the underlying connection strategy themselves, and have strong infrastructure capabilities.

### Price

$1500/month. Please go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase. After subscription, please [contact](https://discord.com/invite/qqJuwRb8Nh) us to begin integration.

### Integration

1. go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase. After subscription, please [contact](https://discord.com/invite/qqJuwRb8Nh) us.
2. Obtain the Block Builder IP and port, and complete the data center deployment or network connectivity preparation as required.
3. Once completed, the client can directly connect to the corresponding address to send requests and test latency, stability, and submission results in a real deployment environment.

### Precautions

Dedicated Connection improves the connection quality between the client and the Builder, but does not guarantee that transactions will be included. The final result is still affected by factors such as market competition, Builder processing strategies, block space, on-chain congestion, and the quality of the transactions.&#x20;

In addition, Dedicated Connection is more suitable for scenarios with clear requirements for network path and connection control. It is recommended to evaluate your own deployment conditions, request patterns, and operational capabilities before using it.
