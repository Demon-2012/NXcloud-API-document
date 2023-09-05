**Brief Description:**
- Report flash call feedback information.
- It is strongly recommended to report to NiuXin Cloud when your customer has entered the verification code and the verification is successful. This can improve our service quality and help us better monitor service anomalies.

**Request URL:**
- `http://api2.nxcloud.com/opt/call/convertion`

**Request Method:**
- GET
```
GET http://api2.nxcloud.com/otp/call/convertion?requestId=xxxxx&action=1
```

**Request Parameters:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| requestId | string | The requestId returned from the flash call verification request interface. |
| action    | int    | 0 for not filled back; 1 for filled back.        |

**Response Parameter Description**

The response is of type `ok`, which is a string.