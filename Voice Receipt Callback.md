**Brief Description:**

- Voice group call/verification (DR) push.

**Request URL:**
- DR push HTTP interface address (provided by the user)
- Example: `http://106.15.34.94:8989/voice/testVoiceDr`

**Request Method:**
- POST (Do not pass the body, submit using form data)

**Parameters:**
*1. Voice group call*

| Parameter          | Required | Type   | Description                                      |
|:-------------------|:---------|:-------|:-------------------------------------------------|
| phone              | Yes      | string | Phone number                                     |
| countryCode        | Yes      | string | Country code                                     |
| duration           | Yes      | string | Connection duration                              |
| voice_type         | Yes      | string | Voice type: 0 for group call, 1 for verification/notification |
| messageid          | Yes      | string | Voice ID, obtained from the successful voice submission |
| basic_price        | Yes      | string | Basic fee for unsuccessful calls                  |
| second             | Yes      | number | Duration in seconds                              |
| cycle              | Yes      | number | Billing cycle                                    |
| size               | Yes      | string | Number of cycles                                 |
| customer_price     | Yes      | string | Customer unit price                              |
| start_time         | No       | string | Call start time                                  |
| end_time           | No       | string | Call end time                                    |
| result             | Yes      | string | Sending result: Successful connection/Unsuccessful connection |
| hangup_cause       | Yes      | string | [Call hangup cause](https://github.com/nxtele/http-api-document/wiki/%E5%91%BC%E5%8F%AB%E6%8C%82%E6%96%AD%E5%8E%9F%E5%9B%A0%E8%A7%A3%E9%87%8A) |
| hangup_disposition | Yes      | string | Termination reason: send_cancel=caller timeout; recv_refuse=called party refusal; recv_bye=called party hangup; send_bye=caller hangup; other=other |
| ivr_result         | Yes      | string | Keypress feedback                                |

*2. Voice verification/notification*

| Parameter          | Required | Type   | Description                                      |
|:-------------------|:---------|:-------|:-------------------------------------------------|
| phone              | Yes      | string | Phone number                                     |
| countryCode        | Yes      | string | Country code                                     |
| duration           | Yes      | string | Connection duration                              |
| voice_type         | Yes      | string | Voice type: 0 for group call, 1 for verification/notification |
| messageid          | Yes      | string | Voice ID, obtained from the successful voice submission |
| second             | Yes      | number | Duration in seconds                              |
| cycle              | Yes      | number | Billing cycle                                    |
| size               | Yes      | string | Number of cycles                                 |
| customer_price     | Yes      | string | Customer unit price                              |
| record_url         | No       | string | Voice record URL, returned during voice verification |
| start_time         | No       | string | Call start time                                  |
| end_time           | No       | string | Call end time                                    |
| result             | Yes      | string | Sending result: Successful connection/Unsuccessful connection |
| hangup_cause       | Yes      | string | [Call hangup cause](https://github.com/nxtele/http-api-document/wiki/%E5%91%BC%E5%8F%AB%E6%8C%82%E6%96%AD%E5%8E%9F%E5%9B%A0%E8%A7%A3%E9%87%8A) |
| hangup_disposition | Yes      | string | Termination reason: send_cancel=caller timeout; recv_refuse=called party refusal; recv_bye=called party hangup; send_bye=caller hangup; other=other |

**Push Example:**

```
http://106.15.34.94:8080/sms/testVoiceDr?phone=8615088888888&countryCode=86&duration=10&voice_type=0&messageid=74078a0090f17e011505297261994&basic_price=0.005&second=10&cycle=60&size=1&customer_price=0.036&start_time=2020-12-01 00:00:00&end_time=2020-12-01 00:00:10&result=Successful connection&hangup_cause=NORMAL_CLEARING&hangup_disposition=send_bye&ivr_result=
```

**User Response:**
- Success: "success"
- Failure: "error"

**Note:**
- The DR is only pushed once. If you need repeated pushes, please contact customer service.