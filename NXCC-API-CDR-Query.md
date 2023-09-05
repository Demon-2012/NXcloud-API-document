# Call Record Query

- URL: `https://api2.nxcloud.com/saas/cc/openapi/cdr/page`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type    | Required | Example Value                    | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | -------------------------------------------------------------------------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki                    | User identity identifier                                                                     |
| ts             | String  | Yes      | 1655710885431                    | Current request timestamp (in milliseconds). The maximum allowed time difference is 60 seconds |
| bizType        | String  | Yes      | 6                                | Business type, fixed value "8"                                                                |
| action         | String  | Yes      | cc                               | Business operation, fixed value "cc"                                                          |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type    | Required | Example Value            | Description                   |
| -------------- | ------- | -------- | ------------------------ | ----------------------------- |
| answered       | Integer | No       | 0                        | Answered: 0 for all, 1 for unanswered, 2 for answered |
| direction      | Integer | No       | 0                        | Call direction: 0 for all, 1 for incoming, 2 for outgoing, 3 for AICC |
| startTime      | Long    | Yes      | 1678894227239            | Start time (timestamp in seconds) |
| endTime        | Long    | Yes      | 1678894227239            | End time (timestamp in seconds) |
| name           | String  | No       | "NX0001"                 | Employee account / agent account |
| caller         | String  | No       | "4444"                   | Caller number |
| callee         | String  | No       | "4444"                   | Callee number |
| callId         | String  | No       | "032f4f81cc7a4e5a902e41f511fbf0e9" | Call ID |
| size           | Integer | Yes      | 100                      | Page size (maximum 100) |
| page           | Integer | Yes      | 1                        | Page number (starting from 1) |



## Request Example

Body (application/json) parameters:

```json
{
  "startTime": 1688140800,
  "endTime": 1690819200,
  "answered": true,
  "direction": 1,
  "name": "NX0001",
  "caller": "4444",
  "callee": "4444",
  "size": 100,
  "page": 1
}
```

## Response Parameters

| Parameter Name | Type    | Description     |
| -------------- | ------- | --------------- |
| code           | Integer | Result code     |
| data           | Object  | Request result  |
| msg            | String  | Request message |

### Successful Response

- data parameter:

| Parameter Name      | Type    | Description                   |
| ------------------- | ------- | ----------------------------- |
| agentName           | String  | Agent account, may be empty    |
| agentNickName       | String  | Agent nickname, may be empty   |
| answered            | Boolean | Whether the call was answered  |
| answerTime          | Long    | Call connection time (timestamp in milliseconds) |
| callDuration        | Integer | Call duration                 |
| callee              | String  | Callee number                 |
| caller              | String  | Caller number                 |
| callId              | String  | Call ID                       |
| direction           | Integer | Call direction, 0: incoming, 1: outgoing, 2: AICC |
| dtmfKeys            | String  | DTMF keys, separated by commas when multiple |
| endTime             | Long    | Call end time (timestamp in milliseconds) |
| hangupBy            | Integer | Hangup party, 0: agent hangup, 1: user hangup, 2: unknown |
| hangupCode          | Integer | Hangup reason code             |
| callStatus          | String  | Call status                   |
| hangupReason        | String  | Hangup reason description     |
| inQueueTime         | Long    | Queue time (timestamp in milliseconds) |
| leaveMsgUrl         | String  | Voicemail URL                 |
| orderId             | String  | Order ID                       |
| other               | String  | Transparent information       |
| intent              | String  | Intent name                   |
| outQueueTime        | Long    | Dequeue time (timestamp in milliseconds) |
| queueDuration       | Integer | Queue duration (in seconds)    |
| recordUrl           | String  | Recording URL                 |
| ringDuration        | Integer | Ring duration (in seconds)     |
| ringTime            | Long    | Call ring time (timestamp in milliseconds) |
| startTime           | Long    | Call start time (timestamp in milliseconds) |
| taskId              | String  | Task ID, displayed for AICC tasks when direction=2 |
| totalCustomerPrice  | Double  | Cost                           |

## Response Example

### Successful Example

```json
{
    "reqId": "a23738fb613d889026fa2c8f4e4378f1",
    "code": 0,
    "msg": "Request succeeded",
    "data": [
        {
            "agentName": null,
            "agentNickName": null,
            "answered": false,
            "answerTime": 0,
            "callDuration": 0,
            "callee": "85235757580",
            "caller": "85215236100",
            "callId": "63b09b9a163616c6c009cb326",
            "direction": 0,
            "dtmfKeys": null,
            "endTime": 1690442498901,
            "hangupBy": 0,
            "hangupCode": 1103,
            "callStatus": "Missed call",
            "hangupReason": "User abandoned the queue",
            "inQueueTime": 1690442492861,
            "leaveMsgUrl": null,
            "orderId": "",
            "other": null,
            "intent": null,
            "outQueueTime": 1690442498000,
            "queueDuration": 5139,
            "recordUrl": null,
            "ringDuration": 6,
            "ringTime": 1690442492000,
            "startTime": 1690442492841,
            "taskId": "",
            "totalCustomerPrice": 0.035
        },
        {
            "agentName": "NX094450006938",
            "agentNickName": "Sample Agent",
            "answered": true,
            "answerTime": 1690423244000,
            "callDuration": 5,
            "callee": "85235757568",
            "caller": "85238531117",
            "callId": "6605fcd9563616c6c009c6240",
            "direction": 0,
            "dtmfKeys": null,
            "endTime": 1690423248124,
            "hangupBy": 1,
            "hangupCode": 1001,
            "callStatus": "Normal termination",
            "hangupReason": "Agent hung up",
            "inQueueTime": 1690423237744,
            "leaveMsgUrl": null,
            "orderId": "",
            "other": null,
            "intent": null,
            "outQueueTime": 1690423244000,
            "queueDuration": 6,
            "recordUrl": "https://*********.mp3",
            "ringDuration": 7,
            "ringTime": 1690423237000,
            "startTime": 1690423237704,
            "taskId": "",
            "totalCustomerPrice": 0.035
        }
    ]
}
```

### Failure Example

```json
{
  "reqId": "FFDD1791E22F4D9DBA967C245C58E544",
  "code": 41000,
  "msg": "End date cannot be empty",
  "data": {}
}
```

## Response Code Explanation

| code      | message  | Solution               |
| --------- | -------- | ---------------------- |
| 0         | Request succeeded |                        |
| 88        | Request failed | Please contact technical support to troubleshoot |
| 99        | System error | Please contact technical support to troubleshoot |
| 1000~100X | Authentication issue | See API authentication section for details |