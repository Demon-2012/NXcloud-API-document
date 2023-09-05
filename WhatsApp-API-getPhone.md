# Query Phone Information
Query WhatsApp phone number information through the API.

- URL: `https://api2.nxcloud.com/api/wa/getPhone`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fmexxx3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | getPhone | WhatsApp business operation, fixed value "getPhone"          |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the WhatsApp application in the NxCloud             |
| business_phones | String | No      | 185xxx99,861xxx24 | WhatsApp numbers of the merchants, separated by ", ". For example: 185xxx99,861xxx24. If the parameter is empty, it returns all number information under the application. |
| messaging_product | String | Yes | whatsapp | Channel for sending messages, must be "whatsapp" for WhatsApp messages |

## Request Example

Body (application/json) parameters:
```json
{
    "business_phones": "185xxx99,861xxx24",
    "appkey": "jh42xxxd434",
    "messaging_product": "whatsapp"
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data JsonObject parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| business_phones | array[business_phone object]| Sequence of phone number information, contains one phone object for the response message with only one number. |

- business_phone object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| display_phone_number | string | Registered WhatsApp number |
| quality_rating       | string | Quality rating of the number |
| verified_name        | string | Display name of the number |
| name_status          | string | Name approval status of the number |
| status               | string | Status of the number |
| current_limit        | string | Current limit for initiating conversations in 24 hours |
| code_verification_status | string | Verification status of the number |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "86xxx24": [
            {
                "display_phone_number": "+86 xxx 24",
                "quality_rating": "GREEN",
                "name_status": "APPROVED",
                "verified_name": "GLORY JACK",
                "code_verification_status": "VERIFIED",
                "current_limit": "",
                "status": "CONNECTED"
            }
        ],
        "1xxx99": [
            {
                "display_phone_number": "+1 xxx99",
                "quality_rating": "GREEN",
                "name_status": "APPROVED",
                "verified_name": "Glory HK",
                "code_verification_status": "NOT_VERIFIED",
                "current_limit": "",
                "status": "CONNECTED"
            }
        ]
    },
    "message": "Request successful"
}
```

### Failed Example
```json
{
    "code": -1,
    "message": "Request failed",
    "data": null
}
```

## Response Code Explanation

| code | message           | Solution                    |
| ---- | ----------------- | --------------------------- |
| 0    | Request successful |                             |
| -1   | Request failed    | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |
| 9000 | Parameter exception | Missing parameters, please check the required parameters |
| 9001 | System business error | Please contact technical support to troubleshoot the issue |
| 9002 | Merchant phone number error | Please confirm if the merchant number belongs to a WhatsApp number |
| 9006 | WhatsApp number not bound to the application | Please contact the business personnel to handle the binding operation between the application and the phone number |