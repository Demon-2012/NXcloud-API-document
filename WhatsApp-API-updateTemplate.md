# Edit Message Template

Edit a specified message template for a specific number under the WhatsApp application.

Please note that if a rich media interactive template was used when creating the template, you need to submit the rich media example file as well. The rich media example file should be uploaded using the "Upload Template Example File" API interface.

- URL: `https://api2.nxcloud.com/api/wa/updateTemplate`
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
| action         | String | Yes      | updateTemplate | WhatsApp business operation, fixed value "updateTemplate"    |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name   | Type   | Required | Example | Description                                                  |
| ---------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey           | String | Yes      |         | Appkey of the NxCloud WhatsApp application                   |
| business_phone   | String | Yes      | 86158xxx1795 | Merchant's WhatsApp number list, including country code, e.g., 185xxx99 |
| messaging_product | String | Yes      | whatsapp | Channel for sending messages, must be "whatsapp" when sending WhatsApp messages |
| category         | String | Yes      | MARKETING | Template type <br>Enum values: <br>"MARKETING": "Includes promotional or discount information, information updates, or invitations for customers to respond/take action. Anything not for utility or authentication purposes is considered marketing",<br>"UTILITY": "Facilitates a specific request or transaction agreed upon by the business, or provides customers with the latest information related to ongoing transactions, including post-purchase notifications and regular bills",<br>"AUTHENTICATION": "Allows merchants to verify user identity using one-time passwords, which may appear in multiple steps of the login process (such as account authentication, account recovery, integrity challenges)" |
| template_id      | String | Yes      |         | Template ID                                                  |
| components       | Array  | Yes      |         | Template components                                          |

- component object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| type           | string | Yes      | Component type, including: HEADER, BODY, FOOTER, BUTTONS     |
| format         | string | Yes/No   | Only required for type=HEADER and not required for other types.<br>Describes the type of content in the HEADER. Possible values: TEXT, DOCUMENT, IMAGE, VIDEO |
| text           | string | Yes/No   | Required for type=HEADER and format=text; Required for type=BODY; Required for type=FOOTER; Not required for type=BUTTONS |
| example        | object | Yes/No   | Variable example. Required when variables are configured in the HEADER or BODY content, otherwise not required |
| buttons        | array  | Yes/No   | Required for type=BUTTONS, otherwise not required            |
| add_security_recommendation | boolean | Yes/No | Add security recommendation. Optional for authentication template with type=BODY. Value: true/false |
| code_expiration_minutes | integer | Yes/No | Expiration time of the verification code. Optional for authentication template with type=FOOTER. The valid range is 1-90. |

- example object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| header_handle  | string | Yes/No   | Required when format=DOCUMENT or format=IMAGE or format=VIDEO in HEADER. Either header_handle or custom_header_handle_url should be provided. If both exist, custom_header_handle_url takes precedence. |
| custom_header_handle_url | string | Yes/No | Required when format=DOCUMENT or format=IMAGE or format=VIDEO in HEADER. Either header_handle or custom_header_handle_url should be provided. If both exist, custom_header_handle_url takes precedence. The recommended media URL should be less than 1MB, otherwise it may time out. |
| header_text    | array  | Yes/No   | Required when format=TEXT in HEADER, otherwise not required   |
| body_text      | array  | Yes/No   | Required when variables are configured in the BODY content. The array may contain one or more values based on the variable configuration. Not required if no variables are configured in the BODY content. |

- button object parameters:

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| type           | string | Yes/No   | Button type, including: QUICK_REPLY, URL, PHONE_NUMBER<br>QUICK_REPLY: Quick reply button;<br>URL: Action call URL button;<br>PHONE_NUMBER: Action call phone number button |
| text           | string | Yes      | Display text of the button                                   |
| url            | string | Yes/No   | URL configured on the action call button. Required only for type=URL. If it is a dynamic URL, it should include the variable suffix {{1}}. |
| phone_number   | string | Yes/No   | Phone number configured on the action call button. Required only for type=PHONE_NUMBER |
| example        | array  | Yes/No   | Example URL. Required for type=URL and dynamic URL, for example: https://www.example.com/user |
| otp_type       | string | Yes/No   | Verification code button type. Fixed values: ONE_TAP or COPY_CODE. ONE_TAP means one-tap autofill, COPY_CODE means copying the verification code |
| autofill_text  | string | Yes/No   | Autofill button text, displayed on the button. Required only for otp_type=ONE_TAP |
| package_name   | string | Yes/No   | Android package name. Required only for otp_type=ONE_TAP       |
| signature_hash | string | Yes/No   | Application hash. Required only for otp_type=ONE_TAP          |

## Request Example
Body (application/json) parameters:
```json
{
	"appkey": "8exxxs",
	"messaging_product": "whatsapp",
	"business_phone": "185xxx99",
	"template_id": "15125xxxx5168",
	"components": [
		{
			"type": "BODY",
			"text": "Your code is {{1}},  please do not share with others update.",
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

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data JsonObject parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| id             | String | Template ID generated by the system |

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
| 9002 | Merchant phone number error | Please confirm whether the merchant number belongs to a WhatsApp number |
| 9006 | The WhatsApp number is not bound to the application | Please contact the business personnel to handle the binding operation between the application and the phone number |