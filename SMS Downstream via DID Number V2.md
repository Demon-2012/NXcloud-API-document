**Brief Description:**

- SMS Downstream via DID Number (V2 version)

**Request Method:**
- URL: `https://api2.nxcloud.com/didsms/mtsend`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

**Additional Information:**
- The customer's SMS upstream push address will also serve as the callback push address for this interface.

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameter Description

### Header Parameters:

| Parameter Name | Type    | Required | Example            | Description                   |
| -------------- | ------- | -------- | ------------------ | ----------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki      | User identity identifier      |
| ts             | String  | Yes      | 1655710885431      | Timestamp of the current request in milliseconds. The maximum time difference allowed between the user and the server is 60 seconds |
| bizType        | String  | Yes      | 4                  | DID business type, fixed value "4" |
| action         | String  | Yes      | mtsend             | DID business operation, fixed value "mtsend" |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:
Parameter Name | Required | Type   | Description
-- | -- | -- | --
sender | Yes | string| DID number (country code + phone number, e.g., 8615088888888)
phone | Yes | string | Receiving phone number (country code + phone number, e.g., 8615088888888). Currently, only single phone numbers are supported for downstream.
content | Yes | string | SMS content to be sent

### Request Example
```
curl --location --request POST 'https://api2.nxcloud.com/didsms/mtsend' \
--header 'accesskey: kGp5uFHN' \
--header 'action: mtsend' \
--header 'biztype: 4' \
--header 'ts: 1655710885431' \
--header 'sign: 6e9506557d1f289501d333ee2c365826' \
--header 'Content-Type: application/json' \
--data-raw '{
    "sender": "8615088888888",
    "phone": "8618637616887",
    "content": "This is a test SMS"
}'
```

## Response Parameter Description

| Parameter Name | Type   | Description       |
| -------------- | ------ | ----------------- |
| message        | string | Request prompt    |
| data           | string | System data       |
| code           | string | Error code        |
| messageId      | string | Message ID        |

### Successful Response Example
```json
{
   "code":0,
   "message":"Success",
   "data":{
      "messageId":"fdgrthtyjujukiulkil646kli6465ilul"
   }
}
```

### Failed Response Example
```json
{
   "code":-1,
   "message":"Failure"
}
```

**Note:**

Business error codes

| Code | Description |
| ---- | ----------- |
| 0    | Success     |
| -1   | Failure     |
| 1001 | Authentication failed (missing public parameters) |
| 1002 | Authentication failed (parameter error) |
| 1003 | Authentication failed (invalid signature) |
| 1004 | Authentication failed (timestamp expired) |
| 1005 | Authentication failed (insufficient authority) |
| 9006 | Phone number parsing error |
| 9007 | Unable to find country configuration |
| 1100 | Customer does not exist / Status is unavailable |
| 1102 | Insufficient balance |
| 12001 | Message content length beyond the limit 1000 |
| 12002 | The number does not belong to you |
| 12004 | Could not find the quote for the DID down SMS with the number not found |
| 12005 | Could not find the quote for the DID down SMS with the vendor not found |
| 12007 | Not find the phone number in the customer number |
| 12008 | Did customer number status exception |