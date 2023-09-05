# Identity Verification Result

Retrieve the result of identity verification through the API.

- URL: `https://api2.nxcloud.com/api/ota/verify`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Calling Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter   | Type   | Required | Example                          | Description                                                  |
| ----------- | ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| accessKey   | String | Yes      | fme2na3kdi3ki                    | User's identity identifier                                   |
| ts          | String | Yes      | 1655710885431                    | Current timestamp of the request (in milliseconds). The maximum time difference allowed between the client and the server is 60 seconds. |
| bizType     | String | Yes      | 6                                | OTA business type, fixed value "6"                          |
| action      | String | Yes      | verify                           | OTA business operation, fixed value "verify"                |
| sign        | String | Yes      | 6e9506557d1f289501d333ee2c365826 | Signature of the API input parameters. [Signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter  | Type   | Required | Example                          | Description                                                  |
| ---------- | ------ | -------- | -------------------------------- | ------------------------------------------------------------ |
| appkey     | String | Yes      | pem28kje                         | Application appkey                                           |
| requestId  | String | Yes      | 989d535f78338411f7de07c028ddee4b | The requestId returned by the one-click login request interface |

## Request Example

Body (application/json) parameters:
```json
{
    "appkey": "pem28kje",
    "requestId": "989d535f78338411f7de07c028ddee4b"
}
```

## Response Parameters

| Parameter | Type       | Description                           |
| --------- | ---------- | ------------------------------------- |
| code      | Integer    | Result code                           |
| data      | JsonObject | Request result                        |
| msg       | String     | Description of the request result      |

### Successful Response
- data parameters:

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| requestId  | String | Request ID                    |
| status     | String | Identity verification result (SUCCESS: success, PENDING: waiting, MISMATCH: mismatch, FAILURE: failure, UNKNOWN: unknown) |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "msg": "Request successful",
    "data": {
        "requestId": "989d535f78338411f7de07c028ddee4b",
        "status": "SUCCESS"
    }
}
```

### Failure Example
```json
{
    "code": 88,
    "msg": "Request failed",
    "data": null
}
```

## Response Code Explanation

| code      | message       | Solution                           |
| --------- | ------------- | ---------------------------------- |
| 0         | Request successful |                                    |
| 88        | Request failed | Please contact technical support to troubleshoot the issue |
| 99        | System error | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |
| 9901      | Parameter error or missing | Parameters are missing, please check the required parameters |
| 9906      | Application does not exist or is not available | Check if the application is created or disabled |
| 9907      | Application has no corresponding quotation | Contact the business personnel to handle the quotation issue |
| 2205      | Message record does not exist | Check if the message exists |
| 2206      | Request is too frequent | The request is too frequent, please try again later |
