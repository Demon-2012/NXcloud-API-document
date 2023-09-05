# Send Message
Initiate WhatsApp number message sending service through API.
- URL: `https://api.nxcloud.com/saas/wa/send`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Request Parameters

### Header Parameters:

| Parameter Name | Type    | Required | Example Value                    | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki                    | User identity identifier                                                                     |
| ts             | String  | Yes      | 1655710885431                    | Current request timestamp (in milliseconds). The maximum allowed time difference is 60 seconds |
| bizType        | String  | Yes      | 2                                | WhatsApp business type, fixed value "2"                                                      |
| action         | String  | Yes      | mt                               | WhatsApp business operation, fixed value "mt"                                                 |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, common convention                                               |

### Body Parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| tenant_id        | Long             | Yes      | 1                        | Tenant ID                     |
| appkey           | String           | Yes      | pem28kje                 | Application appkey            |
| business_phone   | String           | Yes      | 86158xxxx1795            | WhatsApp number of the message sender, including country code. Example: 86158xxxx1795 |
| messaging_product| String           | Yes      | whatsapp                 | Channel for sending messages, must be "whatsapp" for WhatsApp messages |
| recipient_type   | String           | Yes      | individual               | Type of message recipient, must be "individual" for WhatsApp messages |
| to               | String           | Yes      | 86158xxxx1795            | WhatsApp number of the message recipient, including country code. Example: 86158xxxx1795 |
| type             | String           | Yes      | template                 | Type of message to be sent: "template" |
| template         | JsonObject       | Yes      | [Refer to the request example](#template-message) | Template message content, required when type=template |

#### Message Types

Template message parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| template         | JsonObject       | No       | [Refer to the request example](#template-message) | Template message content, required when type=template |

- template object parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| name             | String           | Yes      | -                        | Template name                 |
| language         | JsonObject       | Yes      | -                        | Template language settings    |
| components       | array[component JsonObject] | No | -                 | Sequence of variable settings for template components |

- language object parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| code             | String           | Yes      | -                        | Language code, [refer to supported template languages](#template-languages) |
| policy           | String           | Yes      | -                        | Fixed value: "deterministic"  |

- component object parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| type             | String           | Yes      | -                        | Component type, can be "header" or "body" |
| parameters       | array[parameter JsonObject] | No | -                 | List of component parameter settings |

- parameter object parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| type             | String           | Yes      | -                        | Type of parameter, can be "text" or "image" |
| text             | String           | No       | -                        | Required when type=text, set the text content of the corresponding parameter. Not applicable for other types |
| image            | JsonObject       | No       | -                        | Required when type=image, set the image content of the corresponding parameter. Not applicable for other types |

- image object parameters:

| Parameter Name   | Type             | Required | Example Value            | Description                   |
| ---------------- | ---------------- | -------- | ------------------------ | ----------------------------- |
| link             | String           | Yes      | -                        | URL link of the image. Must be an HTTP/HTTPS URL |

## Request Example
<a name="template-message"></a>
### Refer to the request example

- Template message (parameterized template message)
![Image](https://user-images.githubusercontent.com/38368633/229672634-ffae93c0-f9e0-475e-a710-9873262d0af8.png)

Body (application/json) parameters:
```json
{
    "tenant_id" : 1,
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "template",
    "template": {
		"name": "text_template",
		"language": {
			"code": "en_US",
			"policy": "deterministic"
		},
		"components": [
                        {
				"type": "header",
				"parameters": [{
					"type": "image",
					"image": {
						"link": "https://imglink"
					}
				}]
			}
			{
				"type": "body",
				"parameters": [    // Fill in the parameter text content strictly according to the variable order. Repeat the variable multiple times if necessary.
					{
						"type": "text",  
						"text": "David"  // {{First Name}}
					},
					{
						"type": "text",
						"text": "China"   // {{Country}}
					},
					{
						"type": "text",
						"text": "China"   // {{Country}}
					},
                                        {
						"type": "text",
						"text": "86138XXX"   // {{Phone Number}}
					}
				]
			}
		]
	}
}
```

## Response Parameters

| Parameter Name | Type    | Description     |
| -------------- | ------- | --------------- |
| code           | Integer | Result code     |
| data           | JsonObject | Request result  |
| message        | String  | Request message |
| traceId        | String  | Trace ID        |

- data object parameters:

| Parameter Name | Type    | Description     |
| -------------- | ------- | --------------- |
| message_id     | String  | Message ID      |

## Response Example

### Successful Example
```json
{
	"code": 0,
	"message": "",
	"data": {
		"message_id": "gBGGhSNXV1dfAglVQ0RRuE3YWhc"
	},
	"traceId": "56bf81643292cd6a89ecde64ae00db13"
}
```

## Response Code Explanation

| code      | message           | Solution                    |
| --------- | ----------------- | --------------------------- |
| 0         | Request succeeded |                             |
| -1        | Request failed    | Please contact technical support to troubleshoot |
| 1000~100X | Authentication issue | See API authentication section for details |
21058 | Parameter exception | tenant_id is required |
21059 | Parameter exception | app_key is required |
21060 | Parameter exception | business_phone is required |
21061 | Parameter exception | to (recipient number) is required |
21062 | Parameter exception | type is required, valid values are [template] |
21063 | Parameter exception | template is required |
22020 | Business exception | Customer does not exist |
22041 | Business exception | Failed to send on the cloud platform |
22042 | Business exception | Failed to send WhatsApp message |
22049 | Business exception | Business phone {0} does not exist |
22089 | Business exception | Number not available (No Core App) |
22090 | Business exception | Invalid number |
22091 | Business exception | Not a WhatsApp user |
22092 | Business exception | Language pack does not exist: {0} |
22093 | Business exception | Template does not exist |
22123 | Business exception | Merchant phone number error |
22124 | Business exception | Application does not exist/unavailable |
22122 | Business exception | Application has no corresponding country pricing |
22125 | Business exception | Insufficient account balance |
22126 | Business exception | The WhatsApp number is not bound to the application |
22141 | Business exception | Failed to send WhatsApp, see the message field for details |

<a name="template-languages"></a>
## Template Languages

Language | Code |   | Language | Code |   | Language | Code
-- | -- | -- | -- | -- | -- | -- | --
Afrikaans | af |   | Greek | el |   | Portuguese (BR) | pt_BR
Albanian | sq |   | Gujarati | gu |   | Portuguese (POR) | pt_PT
Arabic | ar |   | Hebrew | he |   | Punjabi | pa
Azerbaijani | az |   | Hindi | hi |   | Romanian | ro
Bengali | bn |   | Hungarian | hu |   | Russian | ru
Bulgarian | bg |   | Indonesian | id |   | Serbian | sr
Catalan | ca |   | Irish | ga |   | Slovak | sk
Chinese (CHN) | zh_CN |   | Italian | it |   | Slovenian | sl
Chinese (HKG) | zh_HK |   | Japanese | ja |   | Spanish | es
Chinese (TAI) | zh_TW |   | Kannada | kn |   | Spanish (ARG) | es_AR
Croatian | hr |   | Kazakh | kk |   | Spanish (SPA) | es_ES
Czech | cs |   | Korean | ko |   | Spanish (MEX) | es_MX
Danish | da |   | Lao | lo |   | Swahili | sw
Dutch | nl |   | Latvian | lv |   | Swedish | sv
English | en |   | Lithuanian | lt |   | Tamil | ta
English (UK) | en_GB |   | Macedonian | mk |   | Telugu | te
English (US) | en_US |   | Malay | ms |   | Thai | th
Estonian | et |   | Marathi | mr |   | Turkish | tr
Filipino | fil |   | Norwegian | nb |   | Ukrainian | uk
Finnish | fi |   | Persian | fa |   | Urdu | ur
French | fr |   | Polish | pl |   | Uzbek | uz
German | de |   |   |   |   | Vietnamese | vi