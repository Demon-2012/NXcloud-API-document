## Summary

- Call Result Push

### Request URL

- Configure the URL provided to the development team.

### Request Method

- Method: POST
- Content-Type: application/json

### Retry Rules

In general, call detail records will be pushed to the specified URL after the call ends. Receiving an HTTP 200 OK indicates that the receipt push has been accepted, and the request is considered completed.
If an HTTP ERROR message is received, NXCLOUD will retry the push every minute for up to 60 minutes. If it fails after 60 minutes, no further retries will be made.

#### Request Body

```json
{
    "id": 45,
    "businessId": "test_busi",
    "customerBindId": "1",
    "bindId": "69f1d1be1a82204c6049b4a2797ed0af",
    "callId": "1604763745256783872",
    "did": "85235757584",
    "caller": "85235757583",
    "callee": "85238533300",
    "callStatus": 1,
    "callStatusMsg": "",
    "duration": 6,
    "startAt": 1671440452,
    "answerAt": 1671440454,
    "hangupAt": 1671440460,
    "hangupCause": "",
    "hangupCode": 0,
    "hangup": 0,
    "recordFile": "https://remote.record.nxcloud.com/pns/20221219/228c76b1-a685-4b26-9e48-a8a1d14670d4.mp3"
}
```

**Receipt Result Explanation**

| Parameter Name | Type   | Description                                  |
| -------------- | ------ | -------------------------------------------- |
| id             | int64  | Call detail record ID                         |
| businessId     | string | Business ID                                   |
| customerBindId | string | Customer bind ID                              |
| bindId         | string | Bind ID                                       |
| callId         | string | Call ID                                       |
| did            | string | DID number                                    |
| caller         | string | Caller's phone number                         |
| callee         | string | Callee's phone number                         |
| callStatus     | int64  | Call status, 0: Unknown, 1: Normal end, 2: Abnormal end |
| callStatusMsg  | string | Call status details (provided by FS)           |
| duration       | int64  | Call duration in seconds                      |
| startAt        | int64  | Call start timestamp in seconds               |
| answerAt       | int64  | Call answer timestamp in seconds              |
| hangupAt       | int64  | Call hangup timestamp in seconds              |
| hangupCause    | string | Hangup cause. Refer to https://www.nxcloud.com/document/nxphone/hang-up-explained |
| hangupCode     | int64  | Q850 description of the error cause. Refer to https://www.nxcloud.com/document/nxphone/hang-up-explained |
| hangup         | int64  | Hangup party, 0: Caller hangup, 1: Callee hangup |
| recordFile     | string | Call recording file URL                        |