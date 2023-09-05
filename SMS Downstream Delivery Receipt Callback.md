**Brief Description:**

- Receipt callback for downlink SMS

**Request URL:**
- The customer's SMS upstream address is also used as the receipt push address.
- For example: `http://did.nxcloud.com/didsms/smsUpPushTest`

**Request Method:**
- POST, submitted in HTTP FORM format
- Content-Type: application/x-www-form-urlencoded

**Parameters:**
- The parameters are the same as the parameters for SMS upstream push, but the meanings are different. Pay attention to the differences.

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|messageId   |Yes|string |SMS ID  |
|type   |Yes|string |SMS type: 0 for upstream, 1 for downstream  |
|toPhone   |Yes|string |Number that received the SMS |
|fromPhone   |Yes|string |Number that sent the SMS |
|content   |Yes|string |Content of the SMS sent |
|size   |Yes|string |Billing count |
|price   |Yes|string |Unit price |
|receiveTime   |Yes|string |Sending time |
|smsStatus   |Yes|string |SMS status: DELIVRD (delivered), UNDELIVR (undelivered) |

**Push Example**

``` 
messageId:fcf3432fd1834ccdac807a7cfb2d1fdf,type:0,toPhone:+18184505018,fromPhone:+12347200160,content:test from wang haha,size:1,price:0.0360,receiveTime:2021-02-07 14:54:00,smsStatus:DELIVRD
```

**User Response**
Return "success" for success.
Return "error" for failure.