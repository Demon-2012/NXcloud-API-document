# Call Log Callback

## Request URL
- HTTP interface address for call log push (configured in **Call Center Settings**)
- Example: `http://your.domain/cc/callback`

## Request Method

- POST

- Method: `POST`

- Content-Type: `application/json`

- Requires authentication: Yes

## Parameters

| Parameter          | Type    | Description                                                  |
| ------------------ | ------- | ------------------------------------------------------------ |
| agentName          | String  | Agent account, may be empty                                  |
| agentNickName      | String  | Agent nickname, may be empty                                 |
| answered           | Boolean | Whether the call was answered                                |
| answerTime         | Long    | Call connection time (timestamp in milliseconds)             |
| callDuration       | Integer | Call duration                                               |
| callee             | String  | Called number                                                |
| caller             | String  | Caller number                                                |
| callId             | String  | Call ID                                                      |
| direction          | Integer | Call direction, 0: Incoming, 1: Outgoing, 2: AICC             |
| dtmfKeys           | String  | DTMF keys, separated by commas when multiple                 |
| endTime            | Long    | Call end time (timestamp in milliseconds)                    |
| hangupBy           | Integer | Hangup party, 0: Agent hangup, 1: User hangup, 2: Unknown     |
| hangupCode         | Integer | Hangup reason code                                            |
| callStatus         | String  | Call status                                                  |
| hangupReason       | String  | Hangup reason description                                    |
| inQueueTime        | Long    | Queue entry time (timestamp in milliseconds)                 |
| leaveMsgUrl        | String  | Voicemail URL                                                |
| orderId            | String  | Order ID                                                     |
| other              | String  | Transparent information                                      |
| intent             | String  | Intent name                                                  |
| outQueueTime       | Long    | Queue exit time (timestamp in milliseconds)                  |
| queueDuration      | Integer | Queue duration (in seconds)                                  |
| recordUrl          | String  | Recording URL                                                |
| ringDuration       | Integer | Ringing duration (in seconds)                                |
| ringTime           | Long    | Call ringing time (timestamp in milliseconds)                |
| startTime          | Long    | Call start time (timestamp in milliseconds)                  |
| taskId             | String  | Task ID, displayed for AICC tasks when direction=2            |
| totalCustomerPrice | Double  | Cost                                                         |

## Push Example

```shell
curl POST '<client_server_address>/callback' \
--header 'token: <token>' \
--header 'Content-Type: application/json' \
--data-raw '{"agentName":"fang.cheng@nxcloud.com","answerTime":1691372192000,"callDuration":7,"callId":"b1920376-5e15-4f22-9996-6233f297685e","callee":"NX09445G000025@43.134.225.234:5060","caller":"85235757581","direction":2,"endTime":1691372213000,"intent":"转人工-成功","orderId":"ORDER_ID","other":"OTHER","startTime":1691372191000,"taskId":"1688363452814331904"}'
```

## User Response
The program determines the success of the push based on the HTTP response status code returned by the customer service.
Success: 200 OK
Failure: Others