**Brief Description:**

- SMS upstream via DID number.

**Request URL:**
- Customer's SMS upstream push address: Provided by the customer. The customer's interface must be written in the following format.
- Example: `http://did.nxcloud.com/didsms/smsUpPushTest`
- This push address will also be used as the delivery receipt push address for SMS downstream.

**Request Method:**
- POST, submitted in HTTP FORM format.
- Content-Type: application/x-www-form-urlencoded

**Parameters:**

| Parameter   | Required | Type   | Description                            |
|:------------|:---------|:-------|:---------------------------------------|
| messageId   | Yes      | string | SMS ID.                                |
| type        | Yes      | string | SMS type: 0 for upstream, 1 for downstream. |
| toPhone     | Yes      | string | Receiving number (DID number) for the SMS. |
| fromPhone   | Yes      | string | Sending number for the SMS.             |
| content     | Yes      | string | Received SMS content.                   |
| size        | Yes      | string | Billing count.                          |
| price       | Yes      | string | Unit price.                             |
| receiveTime | Yes      | string | Receive time.                           |
| smsStatus   | Yes      | string | SMS status: DELIVRD (delivered), UNDELIVR (undelivered). |

**Push Example:**

``` 
messageId:fcf3432fd1834ccdac807a7cfb2d1fdf,toPhone:+18184505018,fromPhone:+12347200160,content:test from wang haha,size:1,price:0.0360,receiveTime:2021-02-07 14:54:00,smsStatus:DELIVRD
```

**User Response:**
- Return "success" for success.
- Return "error" for failure.