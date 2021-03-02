## Cash out api


Cash out service by customers to transfer reward points and loyalty into an actual cash.


## How it works

In rewards system, a user usually would want to cash out their rewards. The equivalent of an actual cash is left for the store owner to decide. But, it simply means: transfer this `X` points into `Y` cash, from `A` card to the user's card `B`.


### API


#### Register

/cashout/register

Register for a new cashout service. This will allow the service provider (you) to delegate us to use your card info on behalf of you to conduct the cashout service.


##### Request

| field | type |
|-------|-------|
| name | string |
| pan | string |
| expDate | string |
| ipin | string |
| consent | bool |
| endpoint | string |

!!! NOTE
 name: provider unique name
 pan: personal account number (16, 19) digits
 expDate: expiration date YYmm format.
 consent: you accept terms of condition and allow us to use your card on behalf of you
 endpoint: remote endpoint we can send the cashout result into


##### Response

Successful transaction
```json
{"result":"ok"}
```

Failed transaction

```json
{"message": "Descriptive text of the error", "code": "error_code"}
```


#### Generate Cash out claim

/cashout/generate/:name

`:name` is the cashout name used in `register`. 

Generate cashout claims is used by the cashout provider backend system to generate claims for their customers.


Request


| field | type |
|-------|------|
| amount | int |
| id | string |

```json
{"amount": 100, "id": "xcx"}
```

!!! NOTE
amount: amount to be cashedout in integer
id: provider specific id for the transaction (to be used by the provider to track their status)

Response

```json
{"result":"2ff61013-b559-4504-9eb7-aa6749c352f0","uuid":"2ff61013-b559-4504-9eb7-aa6749c352f0"}
```

!!! NOTE
    result: uuid result will be used later to build the url
    uuid: uuid response

### Last step

The cashout provider will use the newly generated uuid to build the cashout page for their customers.

In the background, noebs will return the result of the transaction to the `endpoint` provided by the cashout provider.