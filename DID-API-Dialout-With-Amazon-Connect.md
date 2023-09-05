## Using DID to Make Outbound Calls and Transfer to Amazon Connect Agent

- URL: `https://api2.nxcloud.com/did/openapi/amazon/dialout`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the authentication rules at: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type    | Required | Example            | Description                                                                                   |
| -------------- | ------- | -------- | ------------------ | --------------------------------------------------------------------------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki      | User identity identifier                                                                      |
| ts             | String  | Yes      | 1655710885431      | Timestamp of the current request in milliseconds. The maximum allowed time difference is 60 seconds. |
| bizType        | String  | Yes      | 6                  | Business type, fixed value "9"                                                                 |
| action         | String  | Yes      | cc                 | Business operation, fixed value "didaws"                                                      |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name  | Type    | Required | Example        | Description                                      |
| --------------- | ------- | -------- | -------------- | ------------------------------------------------ |
| did             | String  | Yes      | "62xxxxxxxxx"  | DID number from NxCloud                           |
| callee          | String  | Yes      | "62xxxxxxx"    | Terminal callee number                            |
| connectNumber   | String  | Yes      | "65xxxxxxxxx"  | Amazon Connect number                             |
| ringOrder       | String  | No       | 0              | Ringing order, 0: Connect agent first, then call terminal user, 1: Call terminal user first, then connect agent |

## Request Example

Body (application/json) parameters:

```json
{
    "did": "628934**3242",
    "callee": "622678**0001",
    "connectNumber": "6590**39431",
    "ringOrder": 0
}
```

## Response Parameters

| Parameter Name | Type       | Description     |
| -------------- | ---------- | --------------- |
| code           | Integer    | Result code     |
| data           | JsonObject | Request result  |
| msg            | String     | Request message |
| callId         | String     | Call ID         |

## Response Example

### Success Example

```json
{
  "reqId": "9834904964284198A05BE414383621E8",
  "code": 0,
  "msg": "请求成功",
  "data": {
    "callId": "6a1e3d5cbbc675f8b74154e5a0d8f666"
  }
}
```

### Failure Example

```json
{
    "reqId": "78db27d91ebd46e1e52135e2239b03bc",
    "code": 41000,
    "msg": "参数错误或为空",
    "data": {}
}
```

## Response Code Explanation

| code      | message           | Solution                     |
| --------- | ----------------- | ---------------------------- |
| 0         | Request succeeded |                              |
| 88        | Request failed    | Please contact technical support to troubleshoot the issue |
| 99        | System error      | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |