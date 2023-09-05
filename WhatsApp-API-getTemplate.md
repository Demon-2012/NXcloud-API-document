# Query Message Templates
Query the message templates bound to a single number under the WhatsApp application through the API.

- URL: `https://api2.nxcloud.com/api/wa/getTemplate`
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
| action         | String | Yes      | getTemplate | WhatsApp business operation, fixed value "getTemplate"       |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the WhatsApp application in the NxCloud             |
| business_phone | String | Yes      | 86158xxx1795 | WhatsApp number of the merchant, including the country code, e.g., 185xxx99 |
| messaging_product | String | Yes | whatsapp | Channel for sending messages, must be "whatsapp" for WhatsApp messages |
| after          | String | No       |         | Cursor value for pagination, to retrieve the next page of templates |
| before         | String | No       |         | Cursor value for pagination, to retrieve the previous page of templates |
| limit          | Integer| No       |         | Number of templates per page (default value is 20 if empty)   |
| name           | String | No       |         | Template name (returns templates with the same name but different languages) |

## Request Example

Body (application/json) parameters:
```json
{
    "business_phone": "185xxx99",
    "appkey": "jh42xxxd434",
    "messaging_product": "whatsapp"
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
| data           | array[templateInfo object] | Array of template information |
| paging         | object | Pagination information       |

- templateInfo object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| id             | string | Template ID                  |
| category       | string | Template category            |
| language       | string | Template language            |
| name           | string | Template name                |
| status         | string | Template approval status     |
| rejected_reason| string | Reason for rejection         |
| quality_score  | object | Template quality             |
| components     | array[component object] | Template components |

- quality_score object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| score          | string | Template quality score       |

- component object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| type           | string | Component type               |
| format         | string | Format of the component      |
| text           | string | Text content of the component |
| example        | object | Variable examples            |

- example object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| header_handle  | string | Header media resource link   |
| custom_header_handle_url | string | Custom header media resource link |
| header_text    | array[string] | Header text variable examples |
| body_text      | array[string] | Body text variable examples   |

- button object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| type           | string | Button type                  |
| text           | string | Button display text          |
| url            | string | URL configured for the button (only for type=URL) |
| phone_number   | string | Phone number configured for the button (only for type=PHONE_NUMBER) |
| example        | array[string] | Example URLs                |

- paging object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| cursors        | object | Cursors for pagination       |
| next           | string | Next page URL (not empty if there is a next page) |
| previous       | string | Previous page URL (not empty if there is a previous page) |

- cursors object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| before         | string | Cursor value for previous page |
| after          | string | Cursor value for next page   |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "data": [
            {
                "components": [
                    {
                        "format": "TEXT",
                        "text": "ni{{1}}hao",
                        "type": "HEADER",
                        "example": {
                            "header_text": [
                                "AA"
                            ]
                        }
                    },
                    {
                        "text": "hello{{1}}world{{2}}hahah",
                        "type": "BODY",
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
                        "text": "I am footer",
                        "type": "FOOTER"
                    },
                    {
                        "buttons": [
                            {
                                "text": "I am QR1",
                                "type": "QUICK_REPLY"
                            },
                            {
                                "text": "I am QR2",
                                "type": "QUICK_REPLY"
                            }
                        ],
                        "type": "BUTTONS"
                    }
                ],
                "rejected_reason": "INVALID_FORMAT",
                "quality_score": {
                    "score": "UNKNOWN"
                },
                "name": "normal_text3",
                "language": "en_US",
                "id": "15xxxx67",
                "category": "OTP",
                "status": "REJECTED"
            }
        ],
        "paging": {
            "next": "https://graph.facebook.com/v15.0/10xxx925/message_templates?fields=id%2Ccategory%2Clanguage%2Cname%2Cstatus%2Ccomponents%2Crejected_reason%2Cquality_score&limit=20&after=MTkZD",
            "cursors": {
                "before": "MAZDZD",
                "after": "MTkZD"
            }
        }
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