# Shred Stream

### Introduction

Shred Stream delivers shreds at lowest latency to Validators, RPCs, Bots and DeFi Builders.

Based on a global distributed high-performance network, Shred Stream delivers shreds in native UDP packets directly from high-stake validators to clients, minimizing the number of forwarding hops. It is now deployed in Frankfurt, Amsterdam, Tokyo, and New York.

### Price

The price is $500 per data stream per month. Please go to the [Pricing](https://blockrazor.io/#/pricing) page to purchase.

### Instruction

1. Go to [https://www.blockrazor.io/](https://www.blockrazor.io/), click \[Register] in the upper right corner to complete the registration
2. Go to the [Pricing](https://blockrazor.io/#/pricing) page to complete the purchase
3.  Log in to the console, go to Solana - Shred Stream, click Edit, enter IP:Port or domain:Port, and select the region closest to your server.

    <figure><img src="../../../.gitbook/assets/image (77).png" alt=""><figcaption></figcaption></figure>

{% code overflow="wrap" %}
```bash
# Please ensure that the port is open. If your client is deployed on AWS or other cloud services, you should additionally configure inbound rules for the security group
# The steps to open the port are as follows
sudo ufw allow <port>/udp
sudo ufw reload
```
{% endcode %}

4. Complete the payment and return to \[Solana] - \[Shred], click \[Capture] to copy the command

<figure><img src="../../../.gitbook/assets/enode3.png" alt="" width="563"><figcaption></figcaption></figure>

6. Access server to run the command to view the shreds delivered from the relay of Shred Stream
