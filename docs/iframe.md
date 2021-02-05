## iFrame and web integrations in noebs

- Contact noebs team for account creations [mailto:adonese@noebs.dev](mailto:adonese@noebs.dev)
- The team will go with you through simple integration steps, to comply with KYC
    - in the future it will be about sending us a selfie of you + ID cards


## Required fields and API endpoints

`PAYMENT_URL`: https://pay.cashq.app

Our payment checkout is hosted at: [https://pay.cashq.app](pay.cashq.app). The URL for payment will be like this:

`https://pay.cashq.app/:biller_id?id=merchant_defined_id&token=noebs_payment_uuid_token&to=redirect_url_after_payment&hooks=hooks_endpoint_for_post_payment`

Fields:

| field | definition |
|-------|------------|
| id | merchant specific id, for example cart ID |
| token | noebs specific token, UUID |
| url | url to be redirect the user to, after the payment is completed |
| hooks | hooks endpoint, to send the response message to the system |

`token`: is requested from ebs before hand, by calling: PAYMENT_URL/payment_token/:biller_id


### payment token

Endpoint: `https://beta.soluspay.net/api/v1/payment_token/:biller_id`

The request only have `biller_id` as a named url query. `biller_id` is noebs specific biller's name. The response would be like this:

```json
{"result":{"id":"dabceba4-2d23-41d9-9832-f4f005353ce0","uuid":"dabceba4-2d23-41d9-9832-f4f005353ce0"}
```

_NOTE THAT `id` and `uuid` are the same._

**id will be used later as token**

### How the payment scenario works

- User enters to Sara website
- User add items to cart
- User proceed to checkout
- Sara's website performs generate `payment_token` api
- Sara's website parse the corresponding `uuid` from `payment_token`
- **uuid** will be used by Sara as `token`
- Sara can generate the payment token on events like windows.load, or make a dedicated button for that.
- Sara website then will have the sufficient information to complete the payment:
    - payment `token`
    - `amount`
    - `id` (if she has an id for their cart, or 0 for default value)
    - `hooks` (if she want to use noebs webhooks to update her cart system)


Reach out for any help or support. We will publish more examples soon!