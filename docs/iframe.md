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