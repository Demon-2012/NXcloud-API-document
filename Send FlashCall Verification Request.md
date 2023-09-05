**Brief Description:**
- Send FlashCall verification request

**Request URL:**
- `http://api2.nxcloud.com/otp/call/`
- **Note the trailing slash (/) at the end!**

**Request Method:**
- POST http://api2.nxcloud.com/otp/call/
- Content-Type: application/x-www-form-urlencoded  
appkey=aaa&appsecret=bbb&msisdn=62xxxxxxxxx

**Request Parameters:**
  
  |Parameter|Type|Optional|Description|
  |:-----  |:-----|:-----|-----|
  |appkey |string  | Required |App key of the FlashCall application on the NiuXin platform |
  |secretkey |string | Required  |Secret key of the FlashCall application on the NiuXin platform |
  |msisdn |string  | Required |Customer number to be verified |  
  |from |string | Optional  |You can specify the calling number used to dial the user number. The customer will receive a call from this number.<br/> Note that if this number does not exist or has expired, an error code 8 will be returned. |  

**Response Parameter Description:**
  
  |Parameter|Type|Description|
  |:-----  |:-----|-----|
  |code |string   |Result code. 0 indicates success, others indicate failure. Refer to the failure code table for details. |
  |requestId |string   |ID of this request, which can be used to track a verification call |
  |token |string   |Verification code. The last four digits of the number that will be used to dial msisdn |  

- Error codes:

|code|Meaning|
|:-----  |:-----|
|0 |Success   |
|1 |Incorrect appkey/secretkey   |
|2 |Application is disabled   |
|3 |Excessive requests for this application   |
|4 |Insufficient balance   |
|5 |Incorrect msisdn   |
|6 |Excessive requests for the same customer number (msisdn)   |
|7 |Incorrect date and time format. It must be in the format: yyyy-MM-dd HH:mm:ss |
|8 |FlashCall is not available in the country, or the provided from number cannot be used to make calls temporarily |