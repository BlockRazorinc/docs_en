# Curl

#### Request Example <a href="#qing-qiu-shi-li" id="qing-qiu-shi-li"></a>

```bash
curl --request POST \
  --url http://frankfurt.solana.blockrazor.xyz:443/sendBundle \
  --header 'Content-Type: application/json' \
  --header 'apikey: $auth_token' \
  --data '{
  "transactions":["$base64_tx_1","$base64_tx_2","$base64_tx_3"]
}'
```

#### Response Example <a href="#fan-hui-shi-li" id="fan-hui-shi-li"></a>

Normal

```json
{"signature":"$first_tx_signature","error":""}
```

Abnormal

```json
{"signature":"","error":"error: Invalid authentication credentials. Please ensure your auth token is correct and try again"}
```
