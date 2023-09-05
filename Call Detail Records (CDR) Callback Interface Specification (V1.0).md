**Brief Description:**

- Call Detail Records (CDR) Callback Push Interface V1.0

**Push Request URL:**
- Customer development receiving interface for callback push

**Request Method:**
- POST

**Push Parameters:**

| Parameter   | Required | Type     | Description              |
|:------------|:---------|:---------|:-------------------------|
| sessionid   | Yes      | string   | Unique session ID        |
| username    | Yes      | string   | Phone username           |
| mobile_name | Yes      | string   | Phone nickname           |
| sipid       | Yes      | string   | Phone ID                 |
| orderid     | Yes      | string   | Order ID                 |
| code        | Yes      | string   | Country code             |
| phone       | Yes      | string   | Call number              |
| show_phone  | Yes      | string   | Display number           |
| duration    | Yes      | int      | Call duration (in seconds) |
| direction   | Yes      | int      | Call direction: 1 for outgoing, 0 for incoming |
| record      | Yes      | int      | Whether the call is recorded: 0 for not recorded, 1 for recorded |
| record_url  | No       | string   | Recording access address (not the final recording file address [302 redirect]). If you need to fetch the recording file programmatically, first capture the 302 redirect address, and then fetch the recording file from the new address |
| start_time  | Yes      | string   | Start time (Unix timestamp) |
| answer_time | Yes      | string   | Answer time (Unix timestamp) |
| end_time    | Yes      | string   | End time (Unix timestamp) |
| hangup_cause| Yes      | string   | Hangup cause              |

**Push JSON Parameter Example:**

``` 
{"show_phone":"6298881888","direction":0,"end_time":"1555484089","record":1,"answer_time":"1555484086","sipid":"1049002","code":"86","start_time":"1555484075","duration":3,"phone":"4444","username":"6298881888","mobile_name":"first mobile","orderid":"1001233","record_url":"https://as01.nxcloud.com/record/bf1b9043-cb9f-048f-cc97-0f939dc94609","hangup_cause":"NORMAL_CLEARING","sessionid":"bf1b9043-cb9f-048f-cc97-0f939dc94609"} 
```

**Note:**

**Update Notes:**
- Added the `sessionid` field
- Removed the `id` and `fee` fields
- Modified some field names
- Unified the use of timestamps
- Added `mobile_name` field