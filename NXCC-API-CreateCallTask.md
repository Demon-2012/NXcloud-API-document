# Create AI Outbound Task and Add Numbers

- URL: `https://api2.nxcloud.com/saas/cc/openapi/ai/createandcall`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type    | Required | Example                          | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | --------------------------------------------------------------------------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki                    | User identity identifier                                                                      |
| ts             | String  | Yes      | 1655710885431                    | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String  | Yes      | 6                                | Business type, fixed value "8"                                                                 |
| action         | String  | Yes      | cc                               | Business operation, fixed value "cc"                                                          |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name   | Type              | Required | Example         | Description                                                                 |
| ---------------- | ----------------- | -------- | --------------- | --------------------------------------------------------------------------- |
| country          | String            | Yes      | "CN"            | Two-letter country code                                                     |
| taskName         | String            | Yes      | "Task Name"     | Task name                                                                   |
| taskDesc         | String            | No       | "Task Description" | Task description                                                         |
| strategyName     | String            | Yes      | "Default Strategy" | Dialing strategy name, e.g., "One Ring One", "Default Strategy"           |
| dispatchType     | Integer           | Yes      | 0               | Outbound type: 0 - none, 2 - pre-test outbound, 1 - proportional outbound   |
| agentGroupNo     | String            | Yes      | "NXXXXXXXG0000001" | Agent group number                                                         |
| predictCallRate  | Double            | Yes      | 1.0             | Call rate, two decimal places                                               |
| ratioCallRate    | Double            | Yes      | 1.0             | Agent call rate, one decimal place                                          |
| startCount       | Integer           | Yes      | 1               | Algorithm start value                                                       |
| callList         | Array of CallListItem | Yes | []              | User phone numbers                                                          |
| startupType      | Integer           | No       | 0               | Task startup method: 0 - none, 1 - manual start, 2 - scheduled start, 3 - immediate start |

### CallListItem Parameters:
| Parameter Name   | Type              | Required | Example         | Description                                                                 |
| ---------------- | ----------------- | -------- | --------------- | --------------------------------------------------------------------------- |
| orderID          | String            | Yes      | "FFDD1791E22F4D9DBA967C245C58E544" | Unique ID, default UUID                                             |
| userPhone        | String            | Yes      | "86156xxxxxxxx" | Phone number                                                           |
| other            | String            | Yes      | "ebd0788c-a592-49a6-a0e8-3205e0492f54" | Customer pass-through field                                        |


## Request Example

Body (application/json) parameters:

```json
{
    "taskDesc": "Description",
    "callList": [
        {
            "userPhone": "85235757581",
            "other": "OTHER",
            "orderID": "ORDER_ID"
        }
    ],
    "country": "HK",
    "dispatchType": 0,
    "predictCallRate": 1.0,
    "agentGroupNo": "NX09445G000025",
    "taskName": "Task Name",
    "strategyName": "Default Strategy",
    "startCount": 1,
    "ratioCallRate": 1.0,
    "startupType": 3
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| msg            | String     | Request result description |

## Response Example

### Successful Example

```json
{
  "reqId": "9834904964284198A05BE414383621E8",
  "code": 0,
  "msg": "Request successful",
  "data": null
}
```

### Failed Example

```json
{
    "reqId": "78db27d91ebd46e1e52135e2239b03bc",
    "code": 41000,
    "msg": "Parameter error or empty",
    "data": {}
}
```

## Response Code Explanation

| code      | message           | Solution                    |
| --------- | ----------------- | --------------------------- |
| 0         | Request successful |                             |
| 88        | Request failed    | Please contact technical support to troubleshoot the issue |
| 99        | System error      | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |