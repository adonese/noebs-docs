## Cash out api


Cash out service by customers to transfer reward points and loyalty into an actual cash.


## How it works

In rewards system, a user usually would want to cash out their rewards. The equivalent of an actual cash is left for the store owner to decide. But, it simply means: transfer this `X` points into `Y` cash, from `A` card to the user's card `B`.

## API design (draft)

Scenario 1:

- merchant generate token (it needs to be initiated from the client to the merchant)
- merchant system sends us an api token request
- we respond back with a token
- the request will include the card holder name and so
- 


### Register /register

```json

'{"name": "shifa", "endpoint": "http://localhost:8000"}'

```


### Generate token /generate



