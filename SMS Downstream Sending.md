**Brief Description:**

- Downlink SMS Interface

**Request Method:**
- URL: `http://api2.nxcloud.com/api/sms/mtsend`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`
- curl example (With the -d parameter, the HTTP request will automatically add the header Content-Type: application/x-www-form-urlencoded and convert the request to the POST method, so -X POST can be omitted.)
```
curl -d "appkey=1&secretkey=2&phone=123&content=abc" http://api2.nxcloud.com/api/sms/mtsend
```
- Request example reference [HTTP Form Submission](https://github.com/nxtele/http-api-document/wiki/HTTP表单方式提交), [C# Request SMS Interface Code Example](https://github.com/nxtele/http-api-document/wiki/C%23-短信发送接入代码示例)
![postman example](https://images.gitee.com/uploads/images/2021/0624/171916_82b515b9_4760078.jpeg "Dingtalk_2021062417\1539.jpg")


**Parameters:**

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |SMS application appkey  |
|secretkey   |Yes|string |SMS application secretkey  |
|phone   |Yes|string |Recipient number (country code + phone number, e.g., 8615088888888). Multiple numbers can be submitted, separated by commas. If it is a verification code channel SMS application, no more than 5 numbers can be submitted at a time  |
|content   |Yes|string |SMS content, must be URL-encoded (UTF-8), up to 1000 characters |
|source_address   |No|string |sourceaddress (must be 1-20 digits or letters)  |
|sys_messageid   |No|string |User-defined message ID, length between 10-50 characters, type [0-9a-zA-Z-] (This field does not take effect if there are multiple phone numbers)|
|short_link   |No|string |Short link, data comes from the short link list; if assigned here, the SMS content must contain #1# to take effect, please note  |
|linkVerbose   |No|string |This parameter is set to collect user click behavior. If user click behavior is selected, the number information of the clicked short link can be viewed in the console. Parameter: 1: collect; 0: do not collect. The default is to collect|
|dr_url   |No|string |DR push address (If the SMS application also has a DR push address configured, the DR will be pushed to the address configured in this interface; (This field does not take effect if there are multiple phone numbers, please contact NOC to set it to the specific SMS application) |
|ext   |No|string |Transparent field, this field is custom information, and will be returned as it is in the receipt. Only supports HTTP requests (This field does not take effect if there are multiple phone numbers)|
|opt_entity_id   |No|string |Please pass the entity ID (EntityId) registered according to the DLT rules in India (91) |
|opt_template_id   |No|string |Please pass the template ID (TemplateId) registered according to the DLT rules in India (91) |
|opt_header_id   |No|string |Please pass the sender ID (HeaderId) registered according to the DLT rules in India (91) |
 
**Response Example**

``` 
{"result":"Request succeeded","messageid":"20d6c660bd664c65bef20026564b0b79","code":"0"}
```

**Response Parameter Description**

|Parameter|Type|Description|
|:-----  |:-----|-----|
|result |string   |Request result description |
|messageid |string   |System-generated SMS ID |
|code |string   |Result code |

**Note**

- HTTP Error Codes

|code|Description|
|:----- |-----|
|0 |Request succeeded  | 
|1 |Application unavailable or incorrect key   |
|2 |Parameter error or empty   |
|3 |Insufficient balance   |
|4 |Content is empty or contains illegal keywords   |
|5 |Content is too long   |
|6 |Invalid number   |
|8 |sourceaddress/sender must be 1-20 digits or letters   |
|9|Invalid IP |
|27|Frequency limit is enabled, and the maximum allowed number of messages sent to the same number within one hour (5 messages per hour) has been reached |
|28|TPS rate limiting is enabled, and the current traffic has reached the configured TPS rate limit   |
|88 |Request failed  |
|99 |System error   |
|102|The current account or the account of the affiliated agent has been deactivated   |
|104|Verification code channel applications do not allow more than 5 numbers to be submitted at a time   |

-SMPP Submit SMS Error Codes

| code             |Description|
|:-----------------|-----|
| 10  [0x0000000A] |sourceaddress (sender) error |
| 81  [0x00000051] |Number error  |
| 88  [0x00000058] |Frequency limit  |
| 103 [0x00000067] |Insufficient balance|
| 260 [0x00000104] |Content is empty or contains illegal keywords  |
| 69               |Submission failed, unknown error (complain to us, we will check the logs)   |