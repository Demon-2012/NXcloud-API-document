# Send Message

Initiate WhatsApp number message sending service through the API.

- URL: `https://api2.nxcloud.com/api/wa/mt`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters
### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fme2na3kdi3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | mt       | WhatsApp business operation, fixed value "mt"                |
| sign           | String | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the NxCloud WhatsApp application                   |
| business_phone | String | Yes      | 86158xxxx1795 | WhatsApp number of the message sender, including country code. e.g., 86158xxxx1795 |
| messaging_product | String | Yes      | whatsapp | Channel for sending messages, must be "whatsapp" when sending WhatsApp messages |
| recipient_type | String | Yes      | individual | Type of message recipient, must be "individual" when sending WhatsApp messages |
| to             | String | Yes      | 86158xxxx1795 | WhatsApp number of the message recipient, including country code. e.g., 86158xxxx1795 |
| type           | String | Yes      | text    | Type of message to be sent. Supported types:<br>1. text<br>2. image<br>3. video<br>4. audio<br>5. document<br>6. location<br>7. sticker<br>8. template<br>

#### Message Types

1. Text Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| text           | JsonObject | No       | [See Request Example](#text-message-request-example) | Text message content, required when type=text |

- text object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| body           | String | Yes      | -       | Text message body, can include URLs or formatted identifiers. Formatting identifiers are as follows: Bold: *text*; Italic: _text_; Strikethrough: ~text~. |
| preview_url    | boolean | No       | -       | Whether to enable URL preview. Set to true to enable preview, set to false to disable preview. URLs must start with http:// or https:// and only domain-based links are recognized (IP-based links are not recognized). URL preview is a message presentation feature supported by the WhatsApp client. |

***

2. Image Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| image          | JsonObject | No       | [See Request Example](#image-message-request-example) | Image message content, required when type=image |

- image object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| link           | String | No (Either link or id is required) | -       | URL link of the image. Must be an HTTP/HTTPS URL. |
| id             | String | No (Either link or id is required) | -       | Storage ID of the image. Obtained after uploading the file through the Media interface. |
| caption        | String | No       | -       | Image caption. |

***

3. Video Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| video          | JsonObject | No       | [See Request Example](#video-message-request-example) | Video message content, required when type=video |

- video object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| link           | String | No (Either link or id is required) | -       | URL link of the video file. Must be an HTTP/HTTPS URL. |
| id             | String | No (Either link or id is required) | -       | Storage ID of the video file. Obtained after uploading the file through the Media interface. |
| caption        | String | No       | -       | Video caption. |

***

4. Audio Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| audio          | JsonObject | No       | [See Request Example](#audio-message-request-example) | Audio message content, required when type=audio |

- audio object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| link           | String | No (Either link or id is required) | -       | URL link of the audio file. Must be an HTTP/HTTPS URL. |
| id             | String | No (Either link or id is required) | -       | Storage ID of the audio file. Obtained after uploading the file through the Media interface. |

***

5. Document Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| document       | JsonObject | No       | [See Request Example](#document-message-request-example) | Document message content, required when type=document |

- document object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| link           | String | No (Either link or id is required) | -       | URL link of the document file. Must be an HTTP/HTTPS URL. |
| id             | String | No (Either link or id is required) | -       | Storage ID of the document file. Obtained after uploading the file through the Media interface. |
| filename       | String | No       | -       | Document file name. |

***

6. Location Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| location       | JsonObject | No       | [See Request Example](#location-message-request-example) | Location message content, required when type=location |

- location object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| longitude      | Double | Yes      | -       | Longitude information.            |
| latitude       | Double | Yes      | -       | Latitude information.             |
| name           | String | No       | -       | Location name.                    |
| address        | String | No       | -       | Detailed address information.     |

7. Sticker Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| sticker        | JsonObject | No       | [See Request Example](#sticker-message-request-example) | Sticker message content, required when type=sticker |

- sticker object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| link           | String | No (Either link or id is required) | -       | URL link of the sticker file. Must be an HTTP/HTTPS URL. |
| id             | String | No (Either link or id is required) | -       | Storage ID of the sticker file. Obtained after uploading the file through the Media interface. |

8. Template Message Parameters:

| Parameter Name | Type       | Required | Example | Description                       |
| -------------- | ---------- | -------- | ------- | --------------------------------- |
| template       | JsonObject | No       | [See Request Example](#template-message-request-example) | Template message content, required when type=template |

- template object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| name           | String | Yes      | -       | Template name.                    |
| language       | JsonObject | Yes  | -       | Template language settings.       |
| components     | array[component JsonObject] | No | - | Variable settings for template components. |

- language object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| code           | String | Yes      | -       | Language code, [see supported template languages](#template-languages). |
| policy         | String | Yes      | -       | Fixed value: deterministic.       |

- component object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| type           | String | Yes      | -       | Component type, can be header, body, button.<br>1) When type=header, set variable information for the template header;<br>2) When type=body, set variable information for the template content;<br>3) When type=button, set variable information for the template button. |
| sub_type       | String | No       | -       | Button type created, required only when type=button, can be url, quick_reply. No value for other types. |
| index          | String | No       | -       | Button position index, required only when type=button, value range is 0-2. |
| parameters     | array[parameter JsonObject] | No | - | Component parameter list. |

- parameter object parameters:

| Parameter Name | Type   | Required | Example | Description                       |
| -------------- | ------ | -------- | ------- | --------------------------------- |
| type           | String | Yes      | -       | Among:<br>1) When component object's type=header, can be text, image, video, document;<br>2) When component object's type=body, value is text;<br>3) When component object's type=button and sub_type=url, value is text;<br>4) When component object's type=button and sub_type=quick_reply, value is payload. No value for other types. |
| text           | String | No       | -       | Required only when type=text, set the text content of the corresponding parameter. No value for other types. |
| payload        | String | No       | -       | Required only when type=payload, set the payload content of the corresponding parameter. Payload object definition refers to the video message. No value for other types. |
| image          | JsonObject | No    | -       | Required only when type=image, set the image content of the corresponding parameter. Image object definition refers to the image message. No value for other types. |
| video          | JsonObject | No    | -       | Required only when type=video, set the video content of the corresponding parameter. Video object definition refers to the video message. No value for other types. |
| document       | JsonObject | No    | -       | Required only when type=document, set the document content of the corresponding parameter. Document object definition refers to the document message. No value for other types. |

## Request Example

### Text Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "text",
    "text": {
        "body": "text-message-content",
        "preview_url": false
    }
}
```

### Image Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "image",
    "image": {
        "id": "5867096a-a9be-4a56-94d6-89377623b4ac",
        "caption":"image test"
    }
}
```

### Video Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "video",
    "video": {
        "id": "5867096a-a9be-4a56-94d6-89377623b4ac",
        "caption":"video test"
    }
}
```

### Audio Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "audio",
    "audio": {
        "id": "a51ca059-e12e-4838-b28b-d471773efb71"
    }
}
```

### Document Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "document",
    "document": {
        "id": "5867096a-a9be-4a56-94d6-89377623b4ac",
        "filename":"document-test"
    }
}
```

### Location Message Request Example
Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "location",
    "location": {
        "latitude": "22.550802897696343",
        "longitude": "113.93844723701477",
        "name": "广东深圳",
        "address": "科兴科学园"
    }
}
```
### Template Message Request Example
- Template Message (Parameterized Template)

Body (application/json) parameters:
```json
{
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
				"type": "body",
				"parameters": [
					{
						"type": "text",
						"text": "David"
					},
					{
						"type": "text",
						"text": "B520"
					}
				]
			}
		]
	}
}
```
- Template Message (OTP Verification Code)

Body (application/json) parameters:
```json
{
    "appkey": "f543ertg",
    "business_phone": "185xxxx8399",
    "messaging_product": "whatsapp",
    "recipient_type": "individual",
    "to": "86136xxxx9759",
    "type": "template",
    "template": {
        "name": "otp_test_02",
        "language": {
            "policy": "deterministic",
            "code": "zh_CN"
        },
        "components": [
            {
                "type": "body",
                "parameters": [
                    {
                        "type": "text",
                        "text": "123456"
                    }
                ]
            },
            {
                "type": "button",
                "sub_type": "url",
                "index": "0",
                "parameters": [
                    {
                        "type": "text",
                        "text": "123456"
                    }
                ]
            }
        ]
    }
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

### Successful Response
- data object parameters:

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| messaging_product | String | Type of communication channel |
| messages       | array[message JsonObject] | Sequence of messages |

- message object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| id             | String | Unique ID generated by the system |

### Failed Response, Meta Error
- data object parameters:

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| error          | JsonObject | Meta error    |

- error object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| code           | String | Meta code                   |
| message        | String | Meta error message          |
| type           | String | Meta error type             |
| fbtrace_id     | String | Meta trace                  |
| error_data     | JsonObject | Meta error data          |

- error_data object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| messaging_product | String | Type of communication channel |
| details        | String | Meta error details          |


## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "messaging_product": "whatsapp",
        "messages": [
            {
                "id": "gBGHhhdgYFCBnwIJ6QRYvhwQk7Nc"
            }
        ]
    },
    "message": "Request successful"
}
```

### Failed Example
#### NxCloud Failure
```json
{
    "code": -1,
    "message": "Request failed",
    "data": null
}
```
#### Meta Failure
```json
{
    "code": 9099,
    "message": "WhatsApp error",
    "data":{
        "error":{
            "code":100,
            "message":"(#100) Invalid parameter",
            "type":"OAuthException",
            "fbtrace_id":"AmCuD7sOjcEDetBNhlT2cJm",
            "error_data":{
                "messaging_product":"whatsapp",
                "details":"Invalid parameter"
            }
        }
    }
}
```
## Response Code Explanation

| code | message           | Solution                    |
| ---- | ----------------- | --------------------------- |
| 0    | Request successful |                             |
| -1   | Request failed    | NxCloud failure, please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | NxCloud failure, refer to the API authentication section for details |
| 9000 | Parameter exception | NxCloud failure, missing parameters, please check the required parameters |
| 9001 | System business error | NxCloud failure, please contact technical support to troubleshoot the issue |
| 9002 | Merchant phone number error | NxCloud failure, please confirm if the merchant number belongs to a WhatsApp number |
| 9003 | Application does not exist/unavailable | NxCloud failure, please contact business personnel to handle the creation/disabling of the cloud platform application |
| 9004 | No corresponding country pricing for the application | NxCloud failure, please contact business personnel to handle the application pricing issue |
| 9005 | Insufficient account balance | NxCloud failure, please contact business personnel to recharge |
| 9006 | The WhatsApp number is not bound to the application | NxCloud failure, please contact business personnel to handle the binding of the application and phone number |
| 9007 | Downstream communication endpoint exception | NxCloud failure, please contact technical support to troubleshoot the issue |
| 9099 | WhatsApp error | Meta failure, official meta error message |

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