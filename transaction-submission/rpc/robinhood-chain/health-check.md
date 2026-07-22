# Health Check

Send post request to the health endpoint to keep connection alive, the request is as follows:

{% tabs %}
{% tab title="CURL" %}
```bash
curl -X POST 'https://robinhood.blockrazor.io/health' \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <auth-token>" \
-d ""
```
{% endtab %}
{% endtabs %}
