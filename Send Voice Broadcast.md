**Brief Description:**

- Voice group call interface

**Request Method:**
- URL: `http://api.nxcloud.com/api/voiceSms/gpsend`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |Voice application appkey  |
|secretkey   |Yes|string |Voice application secretkey  |
|phone   |Yes|string |Phone number, multiple numbers can be uploaded separated by commas (,)  |
|country_code   |Yes|string |Country code (without the + sign, only digits) |
|show_phone   |Yes|string |Number to be displayed (enter any number of digits, the actual displayed number may be modified)  |
|url   |Yes|string |Voice file URL, obtained from the console |
|task_time   |No|string |Scheduled time in yyyy-MM-dd HH:mm:ss format |
|time_zone   |No|string |Time zone (8, 9, 10, etc.). If task_time is provided, time_zone is required, otherwise task_time is ignored |
|sched_hangup   |No|string |Hang up after a certain number of seconds after the scheduled connection (0 means no limit) |
|sms_appkey   |No|string |SMS application APPKEY |
|msg_content   |No|string |Additional SMS content |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/voiceSms/gpsend' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'phone=6212345678' \
--data-urlencode 'country_code=62' \
--data-urlencode 'show_phone=123456' \
--data-urlencode 'url=https://nxcloud.com/1963370420.m4a'
```

**Response Example:**
```json
{"result":"Request succeeded","messageid":"20d6c660bd664c65bef20026564b0b79","code":"0"}
```

**Response Parameter Description:**

|Parameter|Type|Description|
|:-----  |:-----|-----|
|result |string   |Description of the request result |
|messageid |string   |Voice ID returned by the system |
|code |string   |Result code |

**Note:**

- Error codes

|code|Description|
|:----- |-----|
|0 |Request succeeded  | 
|1 |Application unavailable or key error   |
|2 |Parameter error or empty   |
|3 |Insufficient balance   |
|4 |Content is empty or contains illegal keywords   |
|5 |Content is too long   |
|6 |Invalid phone number   |
|9|Illegal IP   |
|20|URL does not exist   |
|21|Invalid display number   |
|22|Route not available   |
|23|Invalid country code   |
|88 |Request failed  |
|99 |System error   |