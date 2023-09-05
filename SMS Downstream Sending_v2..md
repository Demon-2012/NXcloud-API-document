Downlink SMS Interface
- URL: `https://api2.nxcloud.com/api/sms/mtsend_v2`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: `Yes`

<br/>

## Authentication Mechanism ##

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API接口调用约定)

<br/>

## Request Parameters ##

### Header Parameters: ###

| **Parameter Name** | **Type** | **Required** | **Example Value** | **Description**                                               |
| ------------------ | -------- | ------------ | ----------------- | ------------------------------------------------------------- |
| accessKey          | String   | Yes          | fmexxx3ki         | User identity identifier                                      |
| ts                 | String   | Yes          | 1655710885431     | Current timestamp of the request in milliseconds. The maximum allowed time difference between the user and the server is 60 seconds. |
| bizType            | String   | Yes          | 3                 | Business type, fixed value "3"                                |
| action             | String   | Yes          | mtsend            | Business operation, fixed value "mtsend"                      |
| sign               | String   | Yes          | 6e95xxx826        | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API接口调用约定) |

<br/>

### Body Parameters: ###

| Parameter Name   | Type   | Required | Description                                                                 |
| ---------------- | ------ | -------- | --------------------------------------------------------------------------- |
| appKey           | String | Yes      | SMS application appkey                                                      |
| phone            | String | Yes      | Recipient number (country code + phone number, e.g., 8615088888888). Multiple numbers can be submitted, separated by commas. If it is a verification code channel SMS application, no more than 5 numbers can be submitted at a time. |
| content          | String | Yes      | SMS content, up to 1000 characters                                          |
| sourceAddress    | String | No       | sourceaddress (must be 1-20 digits or letters)                                        |
| sysMessageId     | String | No       | User-defined message ID, length between 10-50 characters, type [0-9a-zA-Z-] (This field does not take effect if there are multiple phone numbers) |
| shortLink        | String | No       | Short link, data comes from the short link list; if assigned here, the SMS content must contain #1# to take effect, please note |
| linkVerbose      | String | No       | This parameter is set to collect user click behavior. If user click behavior is selected, the number information of the clicked short link can be viewed in the console. Parameter: 1: collect; 0: do not collect. The default is to collect |
| drUrl            | String | No       | DR push address (If the SMS application also has a DR push address configured, the DR will be pushed to the address configured in this interface; (This field does not take effect if there are multiple phone numbers, please contact NOC to set it to the specific SMS application) |
| ext              | String | No       | Transparent field, this field is custom information, and will be returned as it is in the receipt. Only supports HTTP requests (This field does not take effect if there are multiple phone numbers) |


<br/>

## Request Example ##
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/sms/mtsend_v2' \
--header 'accessKey: asdfsdf' \
--header 'bizType: 3' \
--header 'action: mtsend' \
--header 'ts: 1683277109072' \
--header 'sign: 324324324234324' \
--header 'Content-Type: application/json' \
--data-raw '{
    "appKey": "appKey",
    "phone": "18651883168",
    "content": "content"
}'
```

<br/>

## Response Parameters ##

| Parameter Name | Type   | Description                   |
| -------------- | ------ | ----------------------------- |
| code           | String | Result code, refer to [Response Code Description](#response-codes) |
| messageid      | String | System-generated SMS ID       |
| result         | String | Request result description     |

<br/>

## Response Example ##

> Success Example

```json
{"result":"Request succeeded","code":"0","messageid":"333444555666"}
```
<br/>

> Failure Example
```json
{"result":"Application unavailable or incorrect key","code":"1","messageid":""}
```

<br/>
<a name="response-codes"></a>

## Response Code Description ##

|code|Description|
|----- |-----|
|0 |Request succeeded  |
|1000~10XX |Refer to [API Authentication Common Error Codes](https://github.com/nxtele/http-api-document/wiki/API接口调用约定#cjcwm) for details |
|1 |Application unavailable or incorrect key   |
|2 |Parameter error or empty   |
|3 |Insufficient balance   |
|4 |Content is empty or contains illegal keywords   |
|5 |Content is too long   |
|6 |Invalid number   |
|8 |sourceaddress/sender must be 1-20 digits or letters   |
|9|Invalid IP   |
|27|Frequency limit is enabled, and the maximum allowed number of messages sent to the same number within one hour (5 messages per hour) has been reached |
|28|TPS rate limiting is enabled, and the current traffic has reached the configured TPS rate limit   |
|88 |Request failed  |
|99 |System error  |
|102|The current account or the account of the affiliated agent has been deactivated  |
|104|Verification code channel applications do not allow more than 5 numbers to be submitted at a time  |