**Brief Description:**

- SMS Upstream Result Push via DID Number
- Callback for SMS Delivery Receipt after SMS Downstream

**Request URL:**
- Customer SMS Upstream Push Address: Provided by the customer, the customer interface must be written in the following format
- Example: `http://did.nxcloud.com/didsms/smsUpPushTest`
- This push address is used for SMS upstream result push and SMS delivery receipt callback after SMS downstream

- Push content format: Configured by the customer in the number configuration on the client side
- Configured in JSON format, the callback will use the parameter format specified in this API document and sign it for the callback.

**Request Method:**
- URL: `http://did.nxcloud.com/didsms/smsUpPushTest`
- Method: `POST`
- Content-Type: `application/json`
- Requires signature: Yes

## Parameter Description

### Header Parameters:

| Parameter Name | Type    | Required | Example            | Description                   |
| -------------- | ------- | -------- | ------------------ | ----------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki      | User identity identifier      |
| ts             | String  | Yes      | 1655710885431      | Timestamp of the current request in milliseconds |
| bizType        | String  | Yes      | 4                  | DID business type, fixed value "4" |
| action         | String  | Yes      | mtsend             | DID business operation, fixed value "dr" or "mo". "dr" is the delivery receipt push for SMS downstream, "mo" is the result push for SMS upstream |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

**Request Parameters:**

| Parameter Name | Required | Type   | Description              |
| -------------- | -------- | ------ | ------------------------ |
| messageId      | Yes      | string | SMS ID                   |
| type           | Yes      | string | SMS type: 0 for upstream, 1 for downstream |
| toPhone        | Yes      | string | Receiving number (DID number) |
| fromPhone      | Yes      | string | Sending number            |
| content        | Yes      | string | Received SMS content      |
| size           | Yes      | string | Billing count             |
| price          | Yes      | string | Unit price                |
| receiveTime    | Yes      | string | Receive time              |
| smsStatus      | Yes      | string | SMS status: DELIVRD (delivered), UNDELIVR (undelivered) |

**Push Example**
``` 
curl --location --request POST 'http://did.nxcloud.com/didsms/smsUpPushTest' \
--header 'accesskey: kGp5uFHN' \
--header 'action: dr' \
--header 'biztype: 4' \
--header 'ts: 1690361994834' \
--header 'sign: d8200fa495be3bcd5fda3bc25502131b' \
--header 'Content-Type: application/json' \
--data-raw '{
    "messageId": "fcf3432fd1834ccdac807a7cfb2d1fdf",
    "toPhone": "18184505018",
    "fromPhone": "12347200160",
    "content": "sunt non nisi",
    "size": "1",
    "price": "0.0360",
    "receiveTime": "2021-02-07 14:54:00",
    "smsStatus": "DELIVRD"
}'
```

**User Response:**
- Return "success" for success
- Return "error" for failure