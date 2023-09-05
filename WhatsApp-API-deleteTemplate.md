# Delete Message Template
Delete the template information with the specified name under a WhatsApp number through the API.

- URL: `https://api2.nxcloud.com/api/wa/deleteTemplate`
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
| action         | String | Yes      | deleteTemplate | WhatsApp business operation, fixed value "deleteTemplate"    |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the WhatsApp application in the NxCloud platform   |
| business_phone | String | Yes      | 86158xxx1795 | Merchant's WhatsApp number list, including the country code, e.g., 185xxx99 |
| messaging_product | String | Yes | whatsapp | Channel for sending messages, must be "whatsapp" for WhatsApp messages |
| name           | String | Yes      | String  | Template name (delete all templates with the same name, including multilingual templates) |

## Request Example

Body (application/json) parameters:
```json
{
    "business_phone": "185xxx99",
    "appkey": "jh42xxxd434",
    "messaging_product": "whatsapp",
    "name": "template"
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data JsonObject parameters:

| Parameter Name | Type    | Description                 |
| -------------- | ------- | --------------------------- |
| success        | boolean | Operation success status. `true` indicates successful deletion, `false` indicates deletion failure. |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "success": true
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