# Webhook

For the provided webhook URL, it supports the delivery of WhatsApp-related push messages for [Status Reply](#status-reply) and [Message Reply](#message-reply) in the WhatsApp business context.

- URL: `webhook_url`
- Method: `POST`
- Content-Type: `application/json`

## Status Reply
For scenarios where messages are sent using the WhatsApp API, it provides the delivery status of the messages.

### Response Parameters
Body parameters:

| Parameter Name | Type                | Description       |
| -------------- | ------------------- | ----------------- |
| statuses       | array of status JsonObject | Result code       |
| business_phone | String              | Business phone number |
| messaging_product | String           | Message type, fixed value "whatsapp" |

- status object parameters:

| Parameter Name | Type                | Description       |
| -------------- | ------------------- | ----------------- |
| conversation   | JsonObject          | Conversation information |
| errors         | array of error JsonObject | Error information |
| recipient_id   | String              | Recipient's WhatsApp ID |
| timestamp      | String              | Callback timestamp |
| status         | String              | Message status: [sent](#message-sent), [delivered](#message-delivered), [read](#message-read), [failed](#message-failed), [deleted](#message-deleted) |
| id             | String              | Message ID |
| costs          | array of cost object | Cost information |

- conversation object parameters:

| Parameter Name        | Type       | Description              |
| --------------------- | ---------- | ------------------------ |
| id                    | String     | Conversation ID          |
| expiration_timestamp | String     | Conversation expiration timestamp |
| origin                | JsonObject | Conversation type information |

- origin object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| type           | String | Conversation type |
```
"marketing": "(Effective from June 1, 2023) Merchants initiate conversations using message templates marked as MARKETING", corresponding to direction=4 (marketing)
"utility": "(Effective from June 1, 2023) Merchants initiate conversations using message templates marked as UTILITY", corresponding to direction=5 (notification)
"authentication": "(Effective from June 1, 2023) Merchants initiate conversations using message templates marked as AUTHENTICATION", corresponding to direction=6 (authentication)
"service": "(Effective from June 1, 2023) Users initiate conversations", corresponding to direction=7 (service)
"referral_conversion": "(Effective from June 1, 2023) (Free) Users initiate conversations by clicking on WhatsApp ads or Facebook Page call-to-action buttons", corresponding to direction=8 (free conversation)
```

- error object parameters:

| Parameter Name | Type    | Description |
| -------------- | ------- | ----------- |
| code           | Integer | Error code  |
| title          | String  | Error message |

- cost object parameters:

| Parameter Name | Type    | Description |
| -------------- | ------- | ----------- |
| currency       | String  | Currency    |
| price          | number  | Customer price (local currency CNY) |
| foreign_price  | number  | Customer price (foreign currency) |
| cdr_type       | Integer | CDR type, starting from June 1, 2023, using 4 (marketing), 5 (notification), 6 (authentication), 7 (service), 8 (free conversation) |
| message_id     | String  | WhatsApp message ID |
| direction      | Integer | Direction, 1 (outbound), 2 (inbound) |

### Response Example
#### Message Sent
```json
{
    "statuses":[
        {
            "id":"wamid.HBgNODYxNzYwNjA1MDgxORUCABEYEjI4RTcyNzFGRDVGQTQwQkQ1RAA=",
            "status":"sent",
            "timestamp":"1660019986",
            "recipient_id":"86176xxxx0819",
            "conversation":{
                "id":"72569257438b471cae074da84bed1b83",
                "expiration_timestamp":"1660106400",
                "origin":{
                    "type":"authentication"
                }
            },
            "costs":[
                {
                    "currency":"USD",
                    "price":0,
                    "foreign_price":0,
                    "cdr_type":4,
                    "message_id":"wamid.HBgNNjI4MTI4MTM3NTYwNBUCABEYEkMzODdBNTEzMTAxNDhFMEI5NQA=",
                    "direction":1
                },
                {
                    "currency":"USD",
                    "price":0.1381,
                    "foreign_price":0.02,
                    "cdr_type":4,
                    "message_id":"wamid.HBgNNjI4MTI4MTM3NTYwNBUCABEYEkMzODdBNTEzMTAxNDhFMEI5NQA=",
                    "direction":1
                }
            ]
        }
    ]
}
```

#### Message Delivered
```json
{
  "statuses": [
    {
      "id": "wamid.HBgNODYxNzYwNjA1MDgxORUCABEYEjI4RTcyNzFGRDVGQTQwQkQ1RAA=",
      "status": "delivered",
      "timestamp": "1660019987",
      "recipient_id": "86176xxxx0819",
      "conversation": {
        "id": "72569257438b471cae074da84bed1b83",
        "origin": {
          "type": "authentication"
        }
      }
    }
  ]
}
```

#### Message Read
```json
{
  "statuses": [
    {
      "id": "wamid.HBgNODYxNzYwNjA1MDgxORUCABEYEjI4RTcyNzFGRDVGQTQwQkQ1RAA=",
      "status": "read",
      "timestamp": "1660019990",
      "recipient_id": "86176xxxx0819"
    }
  ]
}
```

#### Message Failed
```json
{
  "statuses": [
    {
      "errors": [
        {
          "code": 470,
          "title": "Failed to send message because you are outside the support window for freeform messages to this user. Please use a valid HSM notification or reconsider."
        }
      ],
      "id": "ID",
      "recipient_id": "WHATSAPP_ID",
      "status": "failed",
      "timestamp": "TIMESTAMP"
    }
  ]
}
```

#### Message Deleted
```json
{
  "statuses": [
    {
      "id": "ID",
      "recipient_id": "WHATSAPP_ID",
      "status": "deleted",
      "timestamp": "TIMESTAMP",
      "type": "message",
      "message": {
        "recipient_id": "WHATSAPP_ID"
      }
    }
  ]
}
```

## Message Reply
For scenarios where WhatsApp users send messages to merchant numbers, it provides the push of inbound message information.

### Response Parameters
Body parameters:

| Parameter Name | Type                | Description       |
| -------------- | ------------------- | ----------------- |
| contacts       | array of contact JsonObject | Contact information |
| messages       | array of message JsonObject | Inbound messages |
| business_phone | String              | Business phone number |
| messaging_product | String           | Message type, fixed value "whatsapp" |

- contact object parameters:

| Parameter Name | Type                | Description       |
| -------------- | ------------------- | ----------------- |
| profile        | JsonObject          | Profile object    |
| wa_id          | String              | Contact's WhatsApp ID |

- profile object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| name           | String | Profile name |

- message object parameters:

| Parameter Name | Type                | Description       |
| -------------- | ------------------- | ----------------- |
| from           | String              | Sender's WhatsApp ID |
| id             | String              | Message identifier, this ID can be used to mark the message as read |
| timestamp      | String              | Message receive timestamp |
| type           | String              | Supported message types:<br>1. text<br>2. image<br>3. video<br>4. voice<br>5. audio<br>6. document<br>7. location<br>8. sticker |
| cost           | JsonObject          | Cost information |

- cost object parameters:

| Parameter Name | Type    | Description |
| -------------- | ------- | ----------- |
| currency       | String  | Currency    |
| price          | number  | Customer price (local currency CNY) |
| foreign_price  | number  | Customer price (foreign currency) |
| cdr_type       | Integer | CDR type, 4 (marketing), 5 (notification), 6 (authentication), 7 (service), 8 (advertisement promotion) |
| message_id     | String  | WhatsApp message ID |
| direction      | Integer | Direction, 1 (outbound), 2 (inbound) |

- Message Types
1. Text Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| text           | JsonObject | [Refer to response example](#text-message-response-example) Text message content, available when type=text |

- text object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| body           | String | Message text |

***

2. Image Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| image          | JsonObject | [Refer to response example](#image-message-response-example) Image message content, available when type=image |

- image object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |
| caption        | String | Image caption |
| mime_type      | String | MIME type of the media file |
| sha256         | String | Checksum signature of the media file |

***

3. Video Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| video          | JsonObject | [Refer to response example](#video-message-response-example) Video message content, available when type=video |

- video object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |
| caption        | String | Video caption |
| mime_type      | String | MIME type of the media file |
| sha256         | String | Checksum signature of the media file |

***

4. Voice Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| voice          | JsonObject | [Refer to response example](#voice-message-response-example) Voice message content, available when type=voice |

- voice object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |
| mime_type      | String | MIME type of the media file |
| sha256         | String | Checksum signature of the media file |

***

5. Audio Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| audio          | JsonObject | [Refer to response example](#audio-message-response-example) Audio message content, available when type=audio |

- audio object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |
| mime_type      | String | MIME type of the media file |
| sha256         | String | Checksum signature of the media file |

***

6. Document Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| document       | JsonObject | [Refer to response example](#document-message-response-example) Document message content, available when type=document |

- document object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |
| mime_type      | String | MIME type of the media file |
| sha256         | String | Checksum signature of the media file |
| filename       | String | Document file name |

***

7. Location Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| location       | JsonObject | [Refer to response example](#location-message-response-example) Location message content, available when type=location |

- location object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| longitude      | String | Longitude information of the location |
| latitude       | String | Latitude information of the location |
| name           | String | Name of the location |
| address        | String | Detailed address information of the location |

***

8. Sticker Message Parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| sticker        | JsonObject | [Refer to response example](#sticker-message-response-example) Sticker message content, available when type=sticker |

- sticker object parameters:

| Parameter Name | Type   | Description |
| -------------- | ------ | ----------- |
| id             | String | Media storage ID, can be used to retrieve media URL |

### Response Example
#### Text Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQNkLO2ipL1_ZpZ41mwgMHEg",
      "text": {
        "body": "Hello"
      },
      "timestamp": "1663053831",
      "type": "text",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQNkLO2ipL1_ZpZ41mwgMHEg",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Image Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQk5kC-xMSoi3XpEwoF2ZkIg",
      "image": {
        "id": "2bc7102f-5491-40b1-a92f-338303eab9d3",
        "mime_type": "image/jpeg",
        "sha256": "0ed3d9d4db83ed7751314af5f2e9bf008edc49a101bebb9054a97f824cf2136b"
      },
      "timestamp": "1663053029",
      "type": "image",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQk5kC-xMSoi3XpEwoF2ZkIg",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Video Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQysyxXFholwoQ-lCwUTTWfw",
      "timestamp": "1663054466",
      "type": "video",
      "video": {
        "id": "bfc0619d-995e-49da-9869-e911a34c43b9",
        "mime_type": "video/mp4",
        "sha256": "e0ceec95f44fec6282ab02f947ee92dbe481dacf0478618a997580a822acc88b"
      },
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQysyxXFholwoQ-lCwUTTWfw",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Voice Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQyrJn0a5IBKlmHZqf_uAuFw",
      "timestamp": "1663055136",
      "type": "voice",
      "voice": {
        "id": "25fdf335-d846-4e6c-9aa8-35f25abc564c",
        "mime_type": "audio/ogg; codecs=opus",
        "sha256": "f321ac774459c50e376048d6f2c02fc2c14f13be85c5e52a67ec16a358b34de7"
      },
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQyrJn0a5IBKlmHZqf_uAuFw",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Audio Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "audio": {
        "id": "aab95384-fc19-4136-a330-97e1f8a4cb02",
        "mime_type": "audio/mpeg",
        "sha256": "9a73ab6362694fba48a5027c8443ceb34838009601ce480d85f08c600cf520f1"
      },
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQdSLi6R7UCDSsCqNkjrtczg",
      "timestamp": "1663053098",
      "type": "audio",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQdSLi6R7UCDSsCqNkjrtczg",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx819",
  "messaging_product": "whatsapp"
}
```

#### Document Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "document": {
        "caption": "null.txt",
        "filename": "null.txt",
        "id": "806bb2f3-d8cc-4477-8b4d-d89df862f6c0",
        "mime_type": "text/plain",
        "sha256": "90c7bd7c509aa1d68c09a67b9ba2d17022a6861681fbd75c8845ee48193e8646"
      },
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQGvyQjDNptdnjvjN0dkD90Q",
      "timestamp": "1663052759",
      "type": "document",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQGvyQjDNptdnjvjN0dkD90Q",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Location Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQO8HTCPOtJUZLNLRo2dPufw",
      "location": {
        "address": "Shenzhen, Guangdong",
        "latitude": 22.550802897696343,
        "longitude": 113.93844723701477,
        "name": "KFC",
        "url": "http://www.kfc.com.cn"
      },
      "timestamp": "1663053163",
      "type": "location",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQO8HTCPOtJUZLNLRo2dPufw",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```

#### Sticker Message Response Example
```json
{
  "contacts": [
    {
      "profile": {
        "name": "Jay"
      },
      "wa_id": "86176xxxx0819"
    }
  ],
  "messages": [
    {
      "from": "86176xxxx0819",
      "id": "ABGHhhdgYFCBnwIQ1kuKFSU5LfuDxSUPOjKIwA",
      "sticker": {
        "id": "1b0a4c77-c5e7-44fa-b2a3-b69941ed3c64",
        "metadata": {
          "emojis": [
            "☕",
            "🙂"
          ],
          "is-first-party-sticker": 1,
          "sticker-pack-id": "whatsappcuppy"
        },
        "mime_type": "image/webp",
        "sha256": "98267fedaeac67a4cc6b5e18a2444249fba5b6363a690115139675d53a63b0ff"
      },
      "timestamp": "1663054803",
      "type": "sticker",
      "cost": {
                "currency": "USD",
                "price": 0,
                "foreign_price": 0,
                "cdr_type": 4,
                "message_id": "ABGHhhdgYFCBnwIQ1kuKFSU5LfuDxSUPOjKIwA",
                "direction": 1
            }
    }
  ],
  "merchant_phone": "86176xxxx0819",
  "messaging_product": "whatsapp"
}
```