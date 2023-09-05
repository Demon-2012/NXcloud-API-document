# Webhook
Push WhatsApp-related information to the provided webhook URL (currently supports pushing [Message Status](#message-status) and [Template Button Click Callback](#template-button-click-callback)).

- URL: `webhook_url`
- Method: `POST`
- Content-Type: `application/json`

<a name="message-status"></a>
## Message Status

Provides the receipt of message status for the scenarios where the WhatsApp API is used to send messages.

### Response Parameters
Body parameters:

Parameter | Type | Description
-- | -- | --
statuses | array[status JsonObject] | Result codes
business_phone | String | Business phone number
messaging_product | String | Message type, fixed value "whatsapp"

- status object parameters:

Parameter | Type | Description
-- | -- | --
conversation | JsonObject | Conversation information
errors | array[error JsonObject] | Error information
recipient_id | String | Recipient's WhatsApp ID
timestamp | String | Callback timestamp
status | String | Message status, [sent](#sent), [delivered](#delivered), [read](#read), [failed](#failed), [deleted](#deleted)
id | String | Message ID

- conversation object parameters:

Parameter | Type | Description
-- | -- | --
id | String | Conversation ID
expiration_timestamp | String | Conversation expiration timestamp
origin | JsonObject | Conversation type information

- origin object parameters:

Parameter | Type | Description
-- | -- | --
type| String | Conversation type

- error object parameters:

Parameter | Type | Description
-- | -- | --
code| Integer | Error code
title| String | Error message

### Response Example
<a name="sent"></a>
#### Message Sent

```json
{
  "statuses": [
    {
      "id": "wamid.HBgNODYxNzYwNjA1MDgxORUCABEYEjI4RTcyNzFGRDVGQTQwQkQ1RAA=",
      "status": "sent",
      "timestamp": "1660019986",
      "recipient_id": "86176xxxx0819",
      "conversation": {
        "id": "72569257438b471cae074da84bed1b83",
        "expiration_timestamp": "1660106400",
        "origin": {
          "type": "business_initiated"
        }
      }
    }
  ]
}
```
<a name="delivered"></a>
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
          "type": "business_initiated"
        }
      }
    }
  ]
}
```
<a name="read"></a>
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
<a name="failed"></a>
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
<a name="deleted"></a>
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
<a name="template-button-click-callback"></a>
## Template Button Click Callback

Provides the callback for button clicks in template messages sent using the WhatsApp API (only supports callbacks for quick reply buttons in templates).

### Response Parameters
Body parameters:

Parameter | Type | Description
-- | -- | --
contacts| array[contact JsonObject] | Contact information
messages| array[message JsonObject] | Callback information
business_phone | String | Business phone number
messaging_product | String | Message type, fixed value "whatsapp"

- contact object parameters:

Parameter | Type | Description
-- | -- | --
profile| object| Contact information
wa_id| String | WhatsApp ID

- profile object parameters:

Parameter | Type | Description
-- | -- | --
name| String | Name

- message object parameters:

Parameter | Type | Description
-- | -- | --
button| object| Button information
from| String| Sender's WhatsApp number
id | String | Message ID
timestamp| String | Callback timestamp
type| String | Type
wa_ext| String| Parameters, template name, template ID, and other information when sending template messages
context| object| Only included when someone replies to your message. Contains information about the original message, such as the sender's ID and the message's ID
tag_name| String| Tag name

- button object parameters:

Parameter | Type | Description
-- | -- | --
payload| String | Button ID
text| String | Button name

- context object parameters:

Parameter | Type | Description
-- | -- | --
from| String | Sender's ID or message ID when someone replies to your message
id| String | Message ID

### Response Example
<a name="template-button-click-callback-example"></a>

```json
{
    "business_phone":"1xxxxxxxxxx",
    "contacts":[
        {
            "profile":{
                "name":"Name"
            },
            "wa_id":"861xxxxxxxxxx"
        }
    ],
    "messages":[
        {
            "button":{
                "payload":"Button ID",
                "text":"Template Button Name"
            },
           "context":{
                        "from":"185xxxxxx99",
                        "id":"wamid.9ce86df19d7941c3965cac2a131a0b0e"
            },
            "from":"861xxxxxxxx59",
            "id":"wamid.HBgNODYxMzYwMzAxOTc1ORUCABIYFjNFQjA0NUJBNDczOTIzQUZBOUQ0OUEA",
            "timestamp":"1692266760",
            "type":"button",
            "tag_name":"Tag Name",
            "wa_ext":"{\"templateId\":233,\"templateName\":\"Template Name\",\"components\":[{\"type\":\"body\",\"parameters\":[{\"type\":\"text\",\"text\":\"xxxx\"},{\"type\":\"text\",\"text\":\"xxxx\"},{\"type\":\"text\",\"text\":\"xxxxx\"}]}]}"
        }
    ],
    "messaging_product":"whatsapp"
}
```