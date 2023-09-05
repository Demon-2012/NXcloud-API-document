# Send Message
Initiate Viber number message sending service via API.
- URL: `https://api2.nxcloud.com/api/viber/mt`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Calling Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header parameters:

| **Parameter** | **Type** | **Required** | **Example** | **Description** |
| ------------ | ------------ | ------------ | -------------------------------- | ------------------------------------------------------------ |
| accessKey    | String       | Yes           | fme2na3kdi3ki                    | User identity identifier                                                 |
| ts           | String       | Yes           | 1655710885431                    | Current timestamp of the request (in milliseconds). The maximum time difference allowed between the client and the NXCLOUD server is 60 seconds. |
| bizType      | String       | Yes           | 7                                | Viber business type, fixed value "7"                      |
| action       | String       | Yes           | mt                               | Viber business operation, fixed value "mt"                     |
| sign         | String       | Yes           | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
appkey | String | Yes | pem28kje | Application appkey
phone | String | Yes | 86158xxxx1795 | Viber number of the message recipient, including the country code. For example, 86158xxxx1795
functionType | String | Yes | text | Viber message function type. The message supports the following function types:<br> 1. `text` Text<br> 2. `image` Image<br> 3. `text_image` Text + Image<br> 4. `text_image_button` Text + Image + Button<br> 5. `text_button` Text + Button<br> 6. `file` File <br> 7. `video` Video <br> 8. `video_text` Video + Text<br>9. `video_text_button` Video + Text + Button<br>
messageData | JsonObject | Yes | [Refer to the request examples](#request-examples) | Viber message body parameters

#### Message Function Types

1. text:
- [Refer to the text request example](#text-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Transactional | Available billing types (`Transactional`/`Session`)
text | String| Yes | Your code is 989724. | Text message content

***

2. image:
- [Refer to the image request example](#image-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`/`Session`)
image | String| Yes | https://***.jpeg | Image link

***

3. text_image:
- [Refer to the text_image request example](#text_image-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
text | String| Yes | Your code is 989724. | Text message content
image | String| Yes | https://***.jpeg | Image link

***

4. text_image_button:
- [Refer to the text_image_button request example](#text_image_button-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
text | String| Yes | Your code is 989724. | Text message content
image | String| Yes | https://***.jpeg | Image link
buttonText | String| Yes | Click me | Button title
buttonLink | String| Yes | `http://www.viber.com` | Button link

***

5. text_button:
- [Refer to the text_button request example](#text_button-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
text | String| Yes | Your code is 989724. | Text message content
buttonText | String| Yes | Click me | Button title
buttonLink | String| Yes | `http://www.viber.com` | Button link

***

6. file:
- [Refer to the file request example](#file-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Transactional | Available billing types (`Transactional`/`Session`)
fileName | String| Yes | fileName.pdf | File name
fileLink | String| Yes | https://***.pdf | File link
fileType | String| Yes | pdf | File type ([Refer to the supported file types list](#file-type-list))

***

7. video:
- [Refer to the video request example](#video-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
thumbnail | String| Yes | https://***.jpeg | Video thumbnail
videoLink | String| Yes | https://***.mp4 | Video link
videoSize | Number| Yes | 1024 | Video file size (in bytes, cannot exceed 200MB)
duration | Number| Yes | 10 | Video duration (in seconds, cannot exceed 600s)

***

8. video_text:
- [Refer to the video_text request example](#video_text-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
thumbnail | String| Yes | https://***.jpeg | Video thumbnail
videoLink | String| Yes | https://***.mp4 | Video link
videoSize | Number| Yes | 1024 | Video file size (in bytes, cannot exceed 200MB)
duration | Number| Yes | 10 | Video duration (in seconds, cannot exceed 600s)
text | String| Yes | Your code is 989724. | Text message content

***

9. video_text_button:
- [Refer to the video_text_button request example](#video_text_button-request-example)
- messageData parameters:

Parameter | Type | Required | Example | Description
-- | -- | -- | -- | --
rateType | String| Yes | Promotional | Available billing types (`Promotional`)
thumbnail | String| Yes | https://***.jpeg | Video thumbnail
videoLink | String| Yes | https://***.mp4 | Video link
videoSize | Number| Yes | 1024 | Video file size (in bytes, cannot exceed 200MB)
duration | Number| Yes | 10 | Video duration (in seconds, cannot exceed 600s)
text | String| Yes | Your code is 989724. | Text message content
buttonText | String| Yes | Click me | Button title

***

## Request Examples

### Text Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "text",
    "messageData": {
        "rateType": "Transactional",
        "text": "Your code is 989724."
    }
}
```

### Image Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "image",
    "messageData": {
        "rateType": "Promotional",
        "image": "https://***.jpeg"
    }
}
```

### Text + Image Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "text_image",
    "messageData": {
        "rateType": "Promotional",
        "text": "Your code is 989724.",
        "image": "https://***.jpeg"
    }
}
```

### Text + Image + Button Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "text_image_button",
    "messageData": {
        "rateType": "Promotional",
        "text": "Your code is 989724.",
        "image": "https://***.jpeg",
        "buttonText": "Click me",
        "buttonLink": "http://www.viber.com"
    }
}
```

### Text + Button Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "text_button",
    "messageData": {
        "rateType": "Promotional",
        "text": "Your code is 989724.",
        "buttonText": "Click me",
        "buttonLink": "http://www.viber.com"
    }
}
```

### File Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "file",
    "messageData": {
        "rateType": "Transactional",
        "fileType": "pdf",
        "fileName": "fileName.pdf",
        "fileLink": "https://***.pdf"
    }
}
```

### Video Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "video",
    "messageData": {
        "rateType": "Promotional",
        "thumbnail": "https://***.jpeg",
        "videoSize": 882472,
        "duration": 15,
        "videoLink": "https://***.mp4"
    }
}
```

### Video + Text Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "video_text",
    "messageData": {
        "rateType": "Promotional",
        "thumbnail": "https://***.jpeg",
        "videoSize": 882472,
        "duration": 15,
        "videoLink": "https://***.mp4",
        "text": "Your code is 989724."
    }
}
```

### Video + Text + Button Request Example

Body (application/json) parameters:
```json
{
    "appkey": "TexxxP6",
    "phone": "791xxxxx730",
    "functionType": "video_text_button",
    "messageData": {
        "rateType": "Promotional",
        "thumbnail": "https://***.jpeg",
        "videoSize": 882472,
        "duration": 15,
        "videoLink": "https://***.mp4",
        "text": "Your code is 989724.",
        "buttonText": "button text"
    }
}
```

## Response Examples

### Success Example
```json
{
    "code": 0,
    "message": "Success",
    "data": {
        "requestId": "b81e8e9fcbbb422a813863e903de94bd"
    }
}
```

### Failure Example
```json
{
    "code": -1,
    "message": "Failure"
}
```

## Response Code Description

code | message | Solution
-- | -- | --
0 | Success | 
-1 | Failure | Please contact the technical personnel to troubleshoot the issue
1000~100X | Authentication failed | Refer to the API authentication section for details
1100 | Customer does not exist / Status is unavailable | Account status exception, contact the business personnel to handle the account issue
1102 | Insufficient balance | Insufficient account balance, please contact the business personnel to recharge
9000 | Request parameter error | Missing parameters, please check the required parameters
9001 | System business error | System business error, please contact the technical personnel to troubleshoot the issue
9002 | Phone number error | Invalid phone number, please check the correctness of the number
9003 | Customer APP does not exist / Status is unavailable | Application status exception, contact the business personnel to handle the creation/disabling of the cloud platform application
9004 | Customer APP does not have quotation | Application quotation missing, contact the business personnel to handle the application quotation issue
9005 | Missing customer APP routes | Application routes missing, please contact the technical personnel to investigate the routes
9999 | Unknown error | Please contact the technical personnel to troubleshoot the issue

# Appendix
## File Type List
File Type | File Formats | Max File Size
-- | -- | --
Documents | .doc, .docx, .rtf, .dot, .dotx, .odt ,odf, .fodt, .txt, .info | 200MB
PDF | .pdf, .xps, .pdax, .eps  | 200MB
Spreadsheet | .xls, .xlsx, .ods, .fods, .csv, .xlsm, .xltx | 200MB

## Template Description
1. Mandatory template sending countries: Russia (`RU`), Ukraine (`UK`), Belarus (`BY`)
2. Billing rules: For `text` type messages, it must match the template approved by Viber registration review. If it matches successfully, it will be billed as `Transactional`; if it fails to match, it will be billed as `Promotional`.

## Session Description
1. Session Start
When the end user initiates a conversation, sending a message of session type will trigger a 24-hour session window.
2. Session Limitations
- Without a response from the end user, you can send a maximum of 5 consecutive session type messages.
- A single session is limited to sending 60 messages to the user.
- After reaching the limit of 60 messages, the session ends.
- If the user responds, sending a session message at this point will start a new session.
3. Session Billing
- Without starting a session, sending session messages will be billed separately based on the message type (e.g., for `text` type messages, if not within a session, it will be sent as `Session` and billed as `Transactional`).
- When a session is started, the first session message will be billed as `Session`, and subsequent session messages within the session will not be billed.