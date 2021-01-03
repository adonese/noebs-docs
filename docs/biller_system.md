# How to use Solus Biller System


## How to use the new API

#### Request a new token

First you need to initialize the paymnet, to do that head over to this link:


```curl -H "content-type: application/json" -X POST https://api.soluspay.net/api/v1/payment_token```

#### Response

The response is in terms of UUID v4 data. It is secure, and don't collide

```json
{"result":{"id":"dabceba4-2d23-41d9-9832-f4f005353ce0","uuid":"dabceba4-2d23-41d9-9832-f4f005353ce0"},"uuid":"dabceba4-2d23-41d9-9832-f4f005353ce0"}
```

**For now, id is the same as uuid but we might change that in the future. So use uuid for future proof integration.**

- Use `uuid` in response in to build the new url

https://sahil.soluspay.net?id={tawasul_reference_id}&amount={entered_amount}&token={uuid}

For example: http://sahil.soluspay.net/?id=123&token=cf455236-69dd-410e-9996-c828d874d6d4&amount=50

This is the link you will be sharing in your mobile app or your website (iframe) to offer the payment ability.

## Timeouts

- **The uuid timeouts in 1 hr**

## Quering result API

In case, you want to see the previous transactions, we offer a querying api.

We need to use the original `uuid` (the one you inquired and sent through token param) and the biller id assigned to each biller to retrieve the status of a particular transaction.

```curl -H "content-type: application/json" -X POST https://api.soluspay.net/api/v1/info?id={token}&biller={biller_id}```


#### Response

##### Successful response

```json
{"id": "some_uuid_here", "terminalId": "18000377","systemTraceAuditNumber": 76,"clientId": "ACTS","responseMessage": "Approval","responseStatus": "Successful","responseCode": 0,"tranDateTime": "200419085611","tranFee": 1.5,"additionalAmount": -1}
```

##### Failed response

Follows our standard 

```json
{"message": "Descriptive message about the error", "code": "error_class"}
```


**note, in this case, the biller ID for Sahil is: `biller:identifer_id`.**


## Cancel transaction

You can also offer to your users Cancellation or do that automatically.
We need to use the original `uuid` (the one you inquired and sent through token param) to cancel a particular transaction.

```json
curl -H "content-type: application/json" -X POST https://api.soluspay.net/api/v1/cancel?id={token}
```


#### Response

**Always check for status codes**

##### Successful response

```json
{"result": true}
```

##### Failed response

Follows our standard 

```json
{"message": "Descriptive message about the error", "code": "error_class"}
```
