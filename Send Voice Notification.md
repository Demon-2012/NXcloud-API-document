**Brief Description:**

- Voice notification interface

**Request Method:**
- URL: `http://api.nxcloud.com/api/voiceSms/notsend`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

|Parameter|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |Voice application appkey  |
|secretkey   |Yes|string |Voice application secretkey  |
|phone   |Yes|string |Phone number, can be submitted in batches, multiple numbers separated by commas (,) |
|country_code   |Yes|string |Country code (without the + sign, only digits) |
|show_phone   |Yes|string |Number to be displayed (enter any number of digits, the actual displayed number may be modified)  |
|content   |Yes|string |Text content; if you need to broadcast a verification code, separate the digits with '-' (e.g., 1-2-3-4-5-6); the content needs to be URL-encoded (UTF-8) |
|lang   |Yes|string |Language code (refer to the table below), zh (Chinese), only pass the abbreviation in English, such as zh, en |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/voiceSms/notsend' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'phone=6212345678' \
--data-urlencode 'country_code=62' \
--data-urlencode 'show_phone=123456' \
--data-urlencode 'content=asdfghjk'
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

- Language codes

|code|Description|
|:----- |-----|
|af	|Afrikaans   |
|ar	|Arabic   |
|bn	|Bengali   |
|bs	|Bosnian   |
|ca	|Catalan   |
|cs	|Czech   |
|cy	|Welsh   |
|da	|Danish   |
|de	|German   |
|el	|Greek   |
|en	|English   |
|eo	|Esperanto   |
|es	|Spanish   |
|et	|Estonian   |
|fi	|Finnish   |
|fr	|French   |
|gu	|Gujarati   |
|hi	|Hindi   |
|hr	|Croatian   |
|hu	|Hungarian   |
|hy	|Armenian   |
|id	|Indonesian   |
|is	|Icelandic   |
|it	|Italian   |
|ja	|Japanese   |
|jw	|Javanese   |
|km	|Khmer   |
|kn	|Kannada   |
|ko	|Korean   |
|la	|Latin   |
|lv	|Latvian   |
|mk	|Macedonian   |
|ml	|Malayalam   |
|mr	|Marathi   |
|my	|Myanmar(Burmese)   |
|ne	|Nepali   |
|nl	|Dutch   |
|no	|Norwegian   |
|pl	|Polish   |
|pt	|Portuguese   |
|ro	|Romanian   |
|ru	|Russian   |
|si	|Sinhala   |
|sk	|Slovak   |
|sq	|Albanian   |
|sr	|Serbian   |
|su	|Sundanese   |
|sv	|Swedish   |
|sw	|Swahili   |
|ta	|Tamil   |
|te	|Telugu   |
|th	|Thai   |
|tl	|Filipino   |
|tr	|Turkish   |
|uk	|Ukrainian   |
|ur	|Urdu   |
|vi	|Vietnamese   |
|zh	|Chinese   |
|zh-yue	|Chinese-Cantonese   |

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