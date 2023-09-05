# Delete Media File
Delete the file information that has been uploaded to WhatsApp through the API.

- URL: `https://api2.nxcloud.com/api/wa/deleteMedia`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fme2na3kdi3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | deleteMedia | WhatsApp business operation, fixed value "deleteMedia"       |
| sign           | String | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| business_phone | String | Yes      | 86158xxxx1795 | Merchant's phone number, including the country code. e.g., 86158xxxx1795 |
| messaging_product | String | Yes | whatsapp | Channel for sending messages, must be "whatsapp" for WhatsApp messages |
| Media-ID       | String | Yes      | fd81acff-eea8-4d9d-acc9-6c62904d6615 | Media file ID |

## Request Example

Body (application/json) parameters:
```json
{
    "business_phone": "86158xxxx1795",
    "Media-ID": "fd81acff-eea8-4d9d-acc9-6c62904d6615",
    "messaging_product": "whatsapp"
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data object parameters:

| Parameter Name | Type    | Description                 |
| -------------- | ------- | --------------------------- |
| success        | boolean | Success flag                |

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