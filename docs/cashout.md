## Cash out api


Cash out service by customers to transfer reward points and loyalty into an actual cash.


A simple walkthrough for this feature will look like this:

- customer will request a cashout (in *your* app)
- you validate the request and send us a cashout request (including amount and id specific to you)
- we send you a url to conduct this payment. 
- you return the url to *your customer* (as a button in the app)
- your customer clicks on the url and enters their info
- we check the request, and if it works, we run the payment request in the background
- the webpage will be done here for
- upon payment completion:
    - we send you a json response regarding the payment (status, amount, etc)

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


## Web hooks integrations

Noebs cashout supports webhooks, actually for the time being we mandate the use of webhooks. Webhooks allow us to work as a mediator between noebs and our payment providers and as a result it can play greatly in scenarios where a system needs to make an update according to our actions.

The request for the web hooks transaction is:

```json
{"name":"shifa","details":{"response":"Generic Error","code":69,"time":"0001-01-01T00:00:00Z","amount":0}}
```
`name`: is the cashout provder name

!!! NOTE
  This is the request we send in our noebs webhooks.


Details is the interesting part

| field | type |
| ------|------|
| response | string |
| code | integer|
| time | time |
| amount | integer |

These tells the status of each transactions.

### Last step

The cashout provider will use the newly generated uuid to build the cashout page for their customers.

In the background, noebs will return the result of the transaction to the `endpoint` provided by the cashout provider.