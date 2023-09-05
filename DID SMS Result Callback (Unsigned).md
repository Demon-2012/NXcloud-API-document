**Brief Description:**

- SMS Upstream Result Push via DID Number
- Callback for SMS Delivery Receipt after SMS Downstream

**Request URL:**
- Customer SMS Upstream Push Address: Provided by the customer, the customer interface must be written in the following format
- Example: `http://did.nxcloud.com/didsms/smsUpPushTest`
- This push address is used for SMS upstream result push and SMS delivery receipt callback after SMS downstream

**Request Method:**
- POST, submitted in HTTP form format
- Content-Type: application/x-www-form-urlencoded

**Parameters:**

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
messageId=fcf3432fd1834ccdac807a7cfb2d1fdf&toPhone=%2B18184505018&fromPhone=%2B12347200160&content=test+from+wang+haha&size=1&price=0.0360&receiveTime=2021-02-07+14%3A54%3A00&smsStatus=DELIVRD
```

**User Response:**
- Return "success" for success
- Return "error" for failure