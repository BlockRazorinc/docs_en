---
description: >-
  Introduction to BlockRazor Ethereum Transaction Sending Mode and API
  Integration Documentation
metaLinks:
  canonical: ./
  alternates:
    - >-
      https://app.gitbook.com/s/QJcHRn7SY50Ny5UQhXHy/transaction-submission/transaction-sending/ethereum
---

# Ethereum Transaction Sending

### What is Broadcast Tx

Broadcast Tx is a fast transaction sending service provided by BlockRazor to help users send transactions with lower latency. It is part of the Fast ecosystem, but unlike the standard Fast model which requires attaching a tip to the transaction, Broadcast Tx does not require users to pay extra for a tip within the transaction, making it more suitable as a low-barrier, fast sending entry point.

Currently, Broadcast Tx offers methods `SendTx` which are used to send single transactions.

It's important to note that while Broadcast Tx belongs to the Fast ecosystem, it is not equivalent to a private transmission channel with full transaction protection capabilities. Transactions sent via Broadcast Tx still enter the public propagation path and therefore _DO NOT_ have MEV protection capabilities.

### In what scenarios should you choose Broadcast Tx

* No tips needed, lower barrier to entry\
  Unlike the standard Fast model, Broadcast Tx does not require adding tips to transactions, making it more suitable for users who want to quickly integrate but do not want to modify the transaction incentive structure.
* Suitable for scenarios where speed is a requirement but MEV protection is not currently emphasized\
  If your priority is to send transactions out as quickly as possible, rather than hiding transactions or mitigating risks like sandwiches and frontrunnings through private paths, then Broadcast Tx would be a more straightforward option.
