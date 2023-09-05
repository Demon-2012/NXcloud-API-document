# Create Message Template
Create a new message template under a specified WhatsApp number in the WhatsApp application.

- URL: `https://api2.nxcloud.com/api/wa/createTemplate`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fmexxx3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | createTemplate | WhatsApp business operation, fixed value "createTemplate"    |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the WhatsApp application in the NxCloud platform   |
| business_phone | String | Yes      | 86158xxxx1795 | Merchant's WhatsApp number list, including the country code, e.g., 185xxx99 |
| messaging_product | String | Yes | whatsapp | Channel for sending messages, must be "whatsapp" for WhatsApp messages |
| category       | String | Yes      | MARKETING | Template category <br>Enum values: <br>"MARKETING": "Includes promotional or discount information, information updates, or invitations for customers to respond/take action. Anything not for utility or authentication purposes is considered marketing",<br>"UTILITY": "Facilitates a specific request or transaction agreed upon by the business, or provides customers with the latest information related to an ongoing transaction, including post-purchase notifications and regular bills",<br>"AUTHENTICATION": "Allows merchants to verify user identity using one-time passwords, which may appear in multiple steps of the login process (such as account authentication, account recovery, integrity challenges)" |
| language       | String | Yes      | zh_CN   | Language code, e.g., zh_CN                                  |
| name           | String | Yes      |         | Template name                                                |
| components     | array[component object] | Yes | | Template components |

- component object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| type           | string | Yes      | Component type, including: HEADER, BODY, FOOTER, BUTTONS     |
| format         | string | Yes/No   | Only required for type=HEADER and not required for other types.<br>Describes the type of content in the HEADER. Possible values: TEXT, DOCUMENT, IMAGE, VIDEO |
| text           | string | Yes/No   | Required for type=HEADER and format=text; Required for type=BODY; Required for type=FOOTER; Not required for type=BUTTONS |
| example        | object | Yes/No   | Variable example. Required when variables are configured in the HEADER or BODY content. Otherwise, not required. |
| buttons        | array[button object] | Yes/No | Required for type=BUTTONS; Otherwise, not required. |
| add_security_recommendation | boolean | Yes/No | Add security recommendation. Optional for type=BODY in authentication templates. Value: true/false. |
| code_expiration_minutes | integer | Yes/No | Expiration time of the verification code. Optional for type=FOOTER in authentication templates. The valid range is 1-90. |

- example object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| header_handle  | string | Yes/No   | Required when format=DOCUMENT or format=IMAGE or format=VIDEO in HEADER. Either header_handle or custom_header_handle_url should be provided. If both exist, custom_header_handle_url takes precedence. |
| custom_header_handle_url | string | Yes/No | Required when format=DOCUMENT or format=IMAGE or format=VIDEO in HEADER. Either header_handle or custom_header_handle_url should be provided. If both exist, custom_header_handle_url takes precedence. The recommended size for the example media URL is less than 1MB to avoid timeouts. |
| header_text    | array[string] | Yes/No | Required when format=TEXT in HEADER. Not required for other types. |
| body_text      | array[string] | Yes/No | Required when variables are configured in the BODY content. The array may contain one or more values based on the variable configuration. Not required when no variables are configured in the BODY content. |

- button object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| type           | string | Yes/No   | Button type, including: QUICK_REPLY, URL, PHONE_NUMBER<br>QUICK_REPLY: Quick reply button;<br>URL: Action call URL button;<br>PHONE_NUMBER: Action call phone number button |
| text           | string | Yes      | Display text of the button                                   |
| url            | string | Yes/No   | Required for type=URL; Not required for other types. If it is a dynamic URL, it should include the variable suffix {{1}}. |
| phone_number   | string | Yes/No   | Required for type=PHONE_NUMBER; Not required for other types. |
| example        | array[string] | Yes/No | Required for type=URL and dynamic URL. For example: https://www.example.com/user |
| otp_type       | string | Yes/No   | OTP button type. Fixed values: ONE_TAP or COPY_CODE. ONE_TAP means autofill; COPY_CODE means copy the verification code. |
| autofill_text  | string | Yes/No   | Autofill button text. Required when otp_type=ONE_TAP.         |
| package_name   | string | Yes/No   | Android package name. Required when otp_type=ONE_TAP.         |
| signature_hash | string | Yes/No   | Application hash. Required when otp_type=ONE_TAP.             |

## Request Example

- Simple text template
Body (application/json) parameters:
```json
{
    "appkey": "8eoxxxos",
    "messaging_product": "whatsapp",
    "business_phone": "185xxx99",
    "name": "normal_text",
    "category": "MARKETING",
    "language": "zh_CN",
    "components": [
        {
            "type": "BODY",
            "text": "hello world"
        }
    ]
}
```

- Rich template
Body (application/json) parameters:
```json
{
	"appkey": "8exxxos",
	"messaging_product": "whatsapp",
	"business_phone": "185xxx99",
	"name": "normal_text3",
	"category": "MARKETING",
	"language": "en_US",
	"components": [{
			"type": "HEADER",
			"format": "TEXT",
			"text": "ni{{1}}hao",
			"example": {
				"header_text": "AA"
			}
		},
		{
			"type": "BODY",
			"text": "hello{{1}}world{{2}}hahah",
			"example": {
				"body_text": [
					[
                        "BB",
                        "CC"
                    ]
				]
			}
		},
		{
			"type": "FOOTER",
			"text": "I am footer"
		},
		{
			"type": "BUTTONS",
			"buttons": [{
					"type": "QUICK_REPLY",
					"text": "I am QR1"
				},
				{
					"type": "QUICK_REPLY",
					"text": "I am QR2"
				}
			]
		}
	]
}
```

- Header with media template
Body (application/json) parameters:
```json
{
	"appkey": "8exxxos",
	"messaging_product": "whatsapp",
	"business_phone": "185xxx99",
	"name": "otp_1",
	"category": "MARKETING",
	"language": "en_US",
	"components": [{
			"type": "HEADER",
			"format": "IMAGE",
			"example": {
				"header_handle": "4:ZG93bl93YS5xxxg"
			}
		},
		{
			"type": "BODY",
			"text": "hello{{1}}world{{2}}hahah",
			"example": {
				"body_text": [
					[
                        "BB",
                        "CC"
                    ]
				]
			}
		},
		{
			"type": "FOOTER",
			"text": "I am footer"
		},
		{
			"type": "BUTTONS",
			"buttons": [{
					"type": "QUICK_REPLY",
					"text": "I am QR1"
				},
				{
					"type": "QUICK_REPLY",
					"text": "I am QR2"
				}
			]
		}
	]
}
```

- Simple MARKETING template
Body (application/json) parameters:
```json
{
	"appkey": "8exxxs",
	"messaging_product": "whatsapp",
	"business_phone": "185xxx99",
	"name": "otp_test",
	"category": "MARKETING",
	"language": "en",
	"components": [
		{
			"type": "BODY",
			"text": "Your code is {{1}},  please do not share with others.",
			"example": {
				"body_text": [
					[
                        "10086"
                    ]
				]
			}
		}
	]
}
```

- Authentication - COPY_CODE
```
{
    "appkey": "8exxxs",
    "messaging_product": "whatsapp",
    "business_phone": "185xxx99",
    "category": "AUTHENTICATION",
    "name": "otp_test_01",
    "language": "zh_CN",
    "components": [
        {
            "type": "BODY",
            "add_security_recommendation": true
        },
        {
            "type": "FOOTER",
            "code_expiration_minutes": 5
        },
        {
            "type": "BUTTONS",
            "buttons": [
                {
                    "type": "OTP",
                    "otp_type": "COPY_CODE",
                    "text": "Copy Code"
                }
            ]
        }
    ]
}
```
- Authentication - ONE_TAP
```
{
    "appkey": "8exxxs",
    "messaging_product": "whatsapp",
    "business_phone": "185xxx99",
    "category": "AUTHENTICATION",
    "name": "otp_test_02",
    "language": "zh_CN",
    "components": [
        {
            "type": "BODY",
            "add_security_recommendation": true
        },
        {
            "type": "FOOTER",
            "code_expiration_minutes": 5
        },
        {
            "type": "BUTTONS",
            "buttons": [
                {
                    "type": "OTP",
                    "otp_type": "ONE_TAP",
                    "text": "Copy Code2",
                    "autofill_text": "Autofill2",
                    "package_name": "com.example.myapplication",
                    "signature_hash": "K8a%2FAINcGX7"
                }
            ]
        }
    ]
}
```


## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data JsonObject parameters:

| Parameter Name | Type    | Description |
| -------------- | ------- | ----------- |
| id             | String  | Template ID |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "id": "900xxx0755"
    },
    "message": "Request successful"
}
```

### Failed Example
```json
{
    "code": -1,
    "message": "Request failed",
    "data": null
}
```

## Response Code Explanation

| code | message           | Solution                    |
| ---- | ----------------- | --------------------------- |
| 0    | Request successful |                             |
| -1   | Request failed    | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |
| 9000 | Parameter exception | Missing parameters, please check the required parameters |
| 9001 | System business error | Please contact technical support to troubleshoot the issue |
| 9002 | Merchant phone number error | Please confirm if the merchant number belongs to a WhatsApp number |
| 9006 | WhatsApp number not bound to the application | Please contact the business personnel to handle the binding operation between the application and the phone number |

### Supported Template Languages

Language | Code |   | Language | Code |   | Language | Code
-- | -- | -- | -- | -- | -- | -- | --
Afrikaans | af |   | Greek | el |   | Portuguese   (BR) | pt_BR
Albanian | sq |   | Gujarati | gu |   | Portuguese   (POR) | pt_PT
Arabic | ar |   | Hebrew | he |   | Punjabi | pa
Azerbaijani | az |   | Hindi | hi |   | Romanian | ro
Bengali | bn |   | Hungarian | hu |   | Russian | ru
Bulgarian | bg |   | Indonesian | id |   | Serbian | sr
Catalan | ca |   | Irish | ga |   | Slovak | sk
Chinese (CHN) | zh_CN |   | Italian | it |   | Slovenian | sl
Chinese   (HKG) | zh_HK |   | Japanese | ja |   | Spanish | es
Chinese   (TAI) | zh_TW |   | Kannada | kn |   | Spanish   (ARG) | es_AR
Croatian | hr |   | Kazakh | kk |   | Spanish   (SPA) | es_ES
Czech | cs |   | Korean | ko |   | Spanish   (MEX) | es_MX
Danish | da |   | Lao | lo |   | Swahili | sw
Dutch | nl |   | Latvian | lv |   | Swedish | sv
English | en |   | Lithuanian | lt |   | Tamil | ta
English   (UK) | en_GB |   | Macedonian | mk |   | Telugu | te
English   (US) | en_US |   | Malay | ms |   | Thai | th
Estonian | et |   | Marathi | mr |   | Turkish | tr
Filipino | fil |   | Norwegian | nb |   | Ukrainian | uk
Finnish | fi |   | Persian | fa |   | Urdu | ur
French | fr |   | Polish | pl |   | Uzbek | uz
German | de |   |   |   |   | Vietnamese | vi