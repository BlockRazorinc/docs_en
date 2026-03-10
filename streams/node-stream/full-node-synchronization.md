# Full Node Synchronization

### Introduction

{% hint style="info" %}
The Full Node Synchronization service is now available for standalone purchase. Users who subscribes to Tier 2 or higher will receive a free quota (the number of full nodes allowed for connection) based on your plan tier.
{% endhint %}

The full-node synchronization service enables low-latency synchronization for Ethereum clients, leveraging high-performance networks. Different from subscribing to block data streams, Ethereum client can directly establish P2P connections with Relay in nearby areas, which synchronizes the latest blocks to the Ethereum clients through P2P network. Users can obtain the latest block events and world state in the first time.



### Price & Free quota

{% hint style="info" %}
The Full Node Synchronization service is available for separate purchase, and the price of a single enode is detailed in the table below. Users who subscribes to Tier 2 or higher will receive a free quota (the number of full nodes allowed for connection) based on your plan tier.
{% endhint %}

#### Standalone Purchase

| Service Duration | Discount | Price             |
| ---------------- | -------- | ----------------- |
| 1 month          | 100%     | $500(1 \* $500)   |
| 3 months         | 95%      | $1425(3 \* $475)  |
| 6 months         | 90%      | $2700(6 \* $450)  |
| 9 months         | 85%      | $3825(9 \* $425)  |
| 12 months        | 80%      | $4800(12 \* $400) |

#### Free Quota of Subscription Plan

<table><thead><tr><th></th><th width="111.94140625">Tier 4</th><th width="93.140625">Tier 3</th><th width="113.08203125">Tier 2</th><th width="121.97265625">Tier 1</th><th width="131.0390625">Tier 0</th></tr></thead><tbody><tr><td>Number of full nodes allowed to connect</td><td>-</td><td>-</td><td>2</td><td>5</td><td>30</td></tr></tbody></table>



### Relay IP

<table><thead><tr><th width="160">Region</th><th>Availability Zone(AWS)</th><th>Relay Address</th></tr></thead><tbody><tr><td>Frankfurt</td><td>euc1-az2</td><td>35.157.64.49:50051</td></tr><tr><td>Tokyo</td><td>apne1-az4</td><td>54.249.93.63:50051</td></tr><tr><td>Ireland</td><td>euw1-az1</td><td>3.248.65.151:50051</td></tr><tr><td>Virginia</td><td>use1-az4</td><td>52.205.173.134:50051</td></tr></tbody></table>



### Instruction

#### Step 1: Add Enode

**Add Enode for Free**

1. Go to [https://www.blockrazor.io](https://www.blockrazor.io/), click \[Register] in the upper right corner to complete the registration
2. Log in to the Portal, go to \[Pricing], select Tier 2 or above, and click \[Get Started]

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="563"><figcaption></figcaption></figure>

3. Confirm the subscription duration and payment method and complete the payment
4. Go to \[Service] - \[Full Node Sync], click \[Add Enode]

<figure><img src="../../.gitbook/assets/image (3).png" alt="" width="563"><figcaption></figcaption></figure>

5. Select the region where Relay is located (it is recommended to select the region closest to the geographical location of your Geth node), enter the Enode of the Ethereum client that needs to be connected, and click \[Confirm] to complete the addition.

<figure><img src="../../.gitbook/assets/image (4).png" alt="" width="563"><figcaption></figcaption></figure>

6. Return to the Enode list and click \[Copy Relay Enode]



**Purchasing Enode separately**

1. Go to [https://www.blockrazor.io](https://www.blockrazor.io/), click \[Register] in the upper right corner to complete the registration
2. Go to \[Service] - \[Full Node Sync], click \[Add Enode]

<figure><img src="../../.gitbook/assets/image (5).png" alt="" width="563"><figcaption></figcaption></figure>

3. Select the region where Relay is located (it is recommended to select the region closest to the geographical location of your Geth node), enter the Enode of the Ethereum client that needs to be connected, and click \[Confirm]

<figure><img src="../../.gitbook/assets/image (6).png" alt="" width="563"><figcaption></figcaption></figure>

4. Confirm the service duration and payment method and complete the payment
5. Return to the Enode list and click \[Copy Relay Enode]\(Note: the enode is created only when the payment is completed)



#### Step 2:  Open ports to allow relay access

{% hint style="info" %}
If your Ethereum client is deployed on AWS or other cloud services, you should additionally configure inbound rules for the security group.
{% endhint %}

1. Access your own Ethereum client's server and execute commands to set up the firewall to allow Relay access.

```
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="52.205.173.134" port port="30311" protocol="tcp" accept'
```

* "source address" is the IP of Relay which can be acquired from [Relay IP](full-node-synchronization.md#relay-ip)
* The port for the Ethereum client to allow Relay access is generally set as the default, which is 30311. You can modify this based on your own node configuration.



2. Reload the firewall configuration to make the changes take effect.

```
sudo firewall-cmd --reload
```



#### Step 3: Check the connection status（Enable the admin namespace in the Geth node as an example）

1. Wait for 10 minutes, access the Geth node, execute the curl command to check the connection status

```json
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"admin_peers","params":[],"id":1}' http://localhost:8545
```



2. In the returned data, query the Relay Enode address (which can be copied from the Portal). If the address is found, it proves that the connection is successful.

```json
[
    {
        "enode": "enode://9ddacbcca0dc1d1b112d470552acc795fce5c3e9f50983fcd5cee7b47289914295acaef3163bea819bcc967461978425def13595deb7de4063295c40e593f320@52.205.173.134:53754",
        "id": "8be29a75ac2cf81e3aa37ccc119630a9dfc43c88d7b5200398a466f5ef9097c4",
        "name": "Geth/v1.4.5/linux-amd64/go1.21.7",
        "caps": [
            "eth/68"
        ],
        "network": {
            "localAddress": "127.0.0.1:30311",
            "remoteAddress": "52.205.173.134:53754",
            "inbound": true,
            "trusted": false,
            "static": false
        },
        "protocols": {
            "eth": {
                "version": 68
            }
        }
    }
]
```

{% hint style="info" %}
If the connection status is found to be abnormal after inquiry, it may be due to network communication problems between nodes. Please go to [Discord](https://discord.com/invite/qqJuwRb8Nh) to contact us.
{% endhint %}



