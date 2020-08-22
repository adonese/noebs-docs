# How to use Solus Biller System


## How to use the new API

#### Request a new token
# curl -H "content-type: application/json" -X POST https://api.soluspay.net/api/v1/payment_token

#### Response

```json
{"result":{"id":"dabceba4-2d23-41d9-9832-f4f005353ce0","uuid":"dabceba4-2d23-41d9-9832-f4f005353ce0"},"uuid":"dabceba4-2d23-41d9-9832-f4f005353ce0"}
```

- Use `uuid` in response in to build the new url

https://sahil.soluspay.net?id={tawasul_reference_id}&amount=entered_amount&token={uuid}

For example: http://sahil.soluspay.net/?id=123&token=cf455236-69dd-410e-9996-c828d874d6d4&amount=50

The rest is the same as before.

## Timeouts

The uuid timeouts in 1 hr.