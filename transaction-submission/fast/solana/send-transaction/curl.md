---
description: This page describes how to build and send Solana transactions using curl
---

# Curl

### Send Transaction

```json
// below is the example of fast mode

curl --request POST \
  --url http://frankfurt.solana.blockrazor.xyz:443/sendTransaction \
  --header 'Content-Type: application/json' \
  --header 'apikey: $auth_token' \
  --data '{
  "transaction":"$base64_tx",
  "mode":"fast",
  "revertProtection":false
}'
```

### Send Binary Transaction

```json
// below is the example of fast mode

curl --request POST \
  --url http://frankfurt.solana.blockrazor.xyz:443/sendBinaryTransaction \
  --header 'Content-Type: application/json' \
  --header 'apikey: $auth_token' \
  --data '{
  "binaryTransaction":"$binary_tx",
  "mode":"fast",
  "revertProtection":false
}'
```
