# Message Callback Service
Push Viber-related information to the provided webhook URL, including [Message Receipt](#message-receipt) and [Message Reply](#message-reply).

## Message Receipt
After sending a Viber message, receive a callback for the message status.
- URL: `dr_webhook`
- Method: `POST`
- Content-Type: `application/json`

### Receipt Parameters
- Body parameters:

Parameter | Type | Description
-- | -- | --
status | String | Receipt status ([failed](#failed), [delivered](#delivered), [seen](#seen), [expired](#expired))
requestId | String | Message send request identifier
code | Number | Status code ([Status Code Description](#status-code-description))
message | String | Status code information
sendTime | String | Sending time

### Receipt Examples

#### failed
```json
{
    "status": "failed",
    "requestId": "f6a7d49946094857ae02812969a83056",
    "code": 11000,
    "message": "Viber send error",
    "sendTime": "2023-07-13 15:12:11"
}
```

#### delivered
```json
{
    "status": "delivered",
    "requestId": "f6a7d49946094857ae02812969a83056",
    "code": 11001,
    "message": "Viber message has delivered",
    "sendTime": "2023-07-13 15:12:11"
}
```

#### seen
```json
{
    "status": "seen",
    "requestId": "f6a7d49946094857ae02812969a83056",
    "code": 11002,
    "message": "Viber message has seen",
    "sendTime": "2023-07-13 15:12:11"
}
```

#### expired
```json
{
    "status": "expired",
    "requestId": "f6a7d49946094857ae02812969a83056",
    "code": 11003,
    "message": "Viber message has expired",
    "sendTime": "2023-07-13 15:12:11"
}
```

## Message Reply
Push the content of user replies to the client's message (currently only supports user replies to sent messages).
- URL: `message_webhook`
- Method: `POST`
- Content-Type: `application/json`

### Reply Parameters
- Body parameters:

Parameter | Type | Description
-- | -- | --
phone | String | Viber user number with country code
appkey | String | Client application appkey
traceRequestId | String | Message reply corresponding to the client's message request identifier
message | JsonObject | Message body content
sendTime | String | Sending time

- message parameters:

Parameter | Type | Description
-- | -- | --
text | String | Text message
media | String | Media message content
fileName | String | Media name

### Message Reply Examples

#### Text Message

```json
{
    "phone":"791xxxxx30",
    "appkey":"TexxxP6",
    "traceRequestId":"ae2c8ff7a4ee408398cf220e3fc1c199",
    "message":{
        "text":"text test"
    },
    "sendTime":"2023-07-17 14:40:50"
}
```

#### Media Message
```json
{
    "phone":"791xxxxx30",
    "appkey":"TexxxP6",
    "traceRequestId":"ae2c8ff7a4ee408398cf220e3fc1c199",
    "message":{
        "media":"https:media-link",
        "fileName":"xxxx.jpeg"
    },
    "sendTime":"2023-07-17 14:44:09"
}
```

## Status Code Description

code | message | Solution
-- | -- | --
1100 | Customer does not exist / Status is unavailable | Account status exception, contact the business personnel to handle the account issue
1102 | Insufficient balance | Insufficient account balance, please contact the business personnel to recharge
9000 | Request parameter error | Missing parameters, please check the required parameters
9001 | System business error | System business error, please contact the technical personnel to troubleshoot the issue
9002 | Phone number error | Invalid phone number, please check the correctness of the number
9003 | Customer APP does not exist / Status is unavailable | Application status exception, contact the business personnel to handle the creation/disabling of the cloud platform application
9004 | Customer APP does not have quotation | Application quotation missing, contact the business personnel to handle the application quotation issue
9005 | Missing customer APP routes | Application routes missing, please contact the technical personnel to investigate the routes
9999 | Unknown error | Please contact the technical personnel to troubleshoot the issue
11000 | Viber send error | Viber official send failure error message
11001 | Viber message has delivered | Message has been delivered
11002 | Viber message has seen | Message has been read
11003 | Viber message has expired | Message has expired