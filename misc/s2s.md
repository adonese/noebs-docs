## Noebs Integrations

Depending on the clients business case, we have different integration scenarios. 

-	Server to Server Integration
-	Hooks integration / mobile or web integrations
-	SDK integration

## Server to Server
-	You get to access our API endpoints directly
-	JSON request / response
-	IPIN calculations are done in your side

Usually, server is more tailored and suitable when the client already have a backend system. The downside is the key management and encryption. 

### API Integration

Noebs has two schemes for API integrations:
-	HTTPS + RESTful APIs
-	gRPC endpoints

For the REST APIs, the request is the same as for EBS, with one variant in the request header (API-Key)

`Base URL: https://beta.soluspay.net`


#### API Request Sample

`/api/v1/key`

Get public Key for encryption

### Request

| Field | Type |
|-------|-------|
| UUID | string |
| tranDateTime | string* |
| applicationId | string |

* `tranDateTime` is time in ISO8601 format: YYMMDDHHmmss, for example 29/12/2020 T 11:11:00 is translated into: `201229111100`.


## Responses

- 400 (Bad Request)

```json
{
    "message": "Request fields validation error",
    "code": 400,
    "status": "BadRequest",
    "details": [
        {
            "applicationId": "this field is required"
        },
        {
            "UUID": "this field is required"
        }
    ]
}
```

- 502 (EBS Errors)

EBS specific Errors such as insufficient funds, destination errors, etc.

```json
{
    "message": "EBSError",
    "code": 601,
    "status": "EBSError",
    "details": {
        "UUID": "4a6ef7c4-ddfa-42bb-b555-7971e955c01a",
        "responseMessage": "INVALID_APPLICATION_ID",
        "responseStatus": "Failed",
        "responseCode": 601,
        "tranDateTime": "200222113700"
    }
}
```

- 200 (Successful responses)

```json
{
    "ebs_response": {
        "pubKeyValue": "MFwwDQYJKoZIhvcNAQEBBQADSwAwSAJBANx4gKYSMv3CrWWsxdPfxDxFvl+Is/0kc1dvMI1yNWDXI3AgdI4127KMUOv7gmwZ6SnRsHX/KAM0IPRe0+Sa0vMCAwEAAQ==",
        "UUID": "4a6ef7c4-ddfa-42bb-b555-7971e955c01a",
        "responseMessage": "Approved",
        "responseStatus": "Successful",
        "responseCode": 0,
        "tranDateTime": "200222113700"
    }
}
```

**NOTE THAT OUR RESPONSE FOR FAILURE CASES ONLY VARIES FROM EBS IN `ebs_response` FIELD**. The rest is fully compatible with EBS.

### Payment Request 

EBS uses the name Special Payment for online purchases.

#### Request fields




### IPIN Encryption

You can use one of our existing encryption libraries to complete IPIN encryption. You can access it here: https://github.com/adonese/crypto

### Purchase / Payment API


Endpoint: `api/v1/purchase`
Headers:
- `Content-Type: application/json`
- `API-Key` Reserved for future


| Field | Type |
|-------|-------|
| UUID | string |
| tranDateTime | string* |
| applicationId | string |
| PAN | string |
| IPIN | string |
| expDate | string |
| tranCurrency | string |
| tranAmount | number(10,2)* |
| serviceProviderId | string |

** `tranAmount` only accepts 2 digits after the floating point.
** `serviceProviderId` is a biller ID (bank account) for the beneficiary.



* `tranDateTime` is time in ISO8601 format: YYMMDDHHmmss, for example 29/12/2020 T 11:11:00 is translated into: `201229111100`.

### Responses

Same as for key responses.

- 400 (Bad Request)

```json
{
    "message": "Request fields validation error",
    "code": 400,
    "status": "BadRequest",
    "details": [
        {
            "applicationId": "this field is required"
        },
        {
            "UUID": "this field is required"
        }
    ]
}
```

- 502 (EBS Errors)

EBS specific Errors such as insufficient funds, destination errors, etc.

```json
{
    "message": "EBSError",
    "code": 601,
    "status": "EBSError",
    "details": {
        "UUID": "4a6ef7c4-ddfa-42bb-b555-7971e955c01a",
        "responseMessage": "INVALID_APPLICATION_ID",
        "responseStatus": "Failed",
        "responseCode": 601,
        "tranDateTime": "200222113700"
    }
}
```

- 200 (Successful responses)

```json
{
    "ebs_response": {
        "UUID": "4a6ef7c4-ddfa-42bb-b555-7971e955c01a",
        "responseMessage": "Approved",
        "responseStatus": "Successful",
        "responseCode": 0,
        "tranDateTime": "200222113700"
    }
}
```

## gRPC integration

We also have gRPC integrations. Contact us support@noebs.dev if you are interested in integration with gRPC.

### SDK integration

Currently we provide SDKs for: Java, and JavaScript.

You can get Java SDK from