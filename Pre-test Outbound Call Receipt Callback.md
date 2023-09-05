**Brief Description:**

- Used for real-time callback of predictive outbound call information.

**Push Request URL:**
- Provide the callback push URL.

**Request Method:**
- POST

**Push Parameters:**

| Parameter | Required | Type   | Description                                      |
|:----------|:---------|:-------|:-------------------------------------------------|
| type      | Yes      | int    | Category: 1 for agent status, 2 for call status  |
| callid    | Yes      | int    | Access number                                     |
| sipid     | No       | string | Agent phone ID                                    |
| username  | No       | string | Agent phone name                                  |
| agentid   | No       | string | Agent UUID                                        |
| state     | Yes      | int    | Status code: 0 for agent hung up, 1 for call creation, 2 for agent waiting for call, 3 for call connected, 4 for call hung up |
| info      | Yes      | string | Status information: 0 for Seats hung up, 1 for Phone calling, 2 for Seats ready, 3 for Phone seats answer, 4 for Phone seats hung up |
| time      | Yes      | string | Status time (Unix timestamp)                      |
| callphone | No       | string | Called number                                    |
| uuid      | No       | string | UUID                                              |

**Push JSON Parameter Example:**
```
{"info":"Seats ready","time":"1558677726435364","callid":"104906","type":1,"agentid":"88e64026-d56b-4dc5-829c-7a7a9f2a1485","state":2,"sipid":"1049002","username":"6122312312"}
{"info":"Phone answer","time":"1558677793395365","uuid":"5c6f5869-752d-46fd-8ac0-797f83222279","state":3,"type":1,"callid":"104906","callphone":"812345613","agentid":"88e64026-d56b-4dc5-829c-7a7a9f2a1485","sipid":"1049002","username":"6122312312"}
{"info":"Phone calling","time":"1558677782655356","callphone":"812345613","callid":"104906","type":2,"uuid":"5c6f5869-752d-46fd-8ac0-797f83222279","state":1}
{"info":"Phone answer","time":"1558677793055398","callphone":"812345613","callid":"104906","type":2,"uuid":"5c6f5869-752d-46fd-8ac0-797f83222279","state":3}
{"info":"Phone hungup","time":"1558678152815399","callphone":"812345613","callid":"104906","type":2,"uuid":"5c6f5869-752d-46fd-8ac0-797f83222279","state":4}
{"info":"Phone hungup","time":"1558678152815399","uuid":"5c6f5869-752d-46fd-8ac0-797f83222279","state":4,"type":1,"callid":"104906","callphone":"812345613","agentid":"88e64026-d56b-4dc5-829c-7a7a9f2a1485","sipid":"1049002","username":"6122312312"}
```

**Note:**
- None.