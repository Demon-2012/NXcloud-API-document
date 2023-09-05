# Integrator Login
Initiate the login service through the API (for integrators only).

- URL: `https://api2.nxcloud.com/api/wa/integrator/embedded/register/login`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters

### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fme2na3kdi3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | login    | WhatsApp business operation, fixed value "login"             |
| sign           | String | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters: None

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| token          | String | Embedded page login token    |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "data": {
        "token": "50abe943xxxe26128e56b08"
    },
    "message": "Request successful"
}
```

### Failed Example
```json
{
    "code": -1,
    "message": "Request failed",
    "data": null
}
```

## Response Code Explanation

| code | message           | Solution                    |
| ---- | ----------------- | --------------------------- |
| 0    | Request successful |                             |
| -1   | Request failed    | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |
| 9000 | Parameter exception | Missing parameters, please check the required parameters |
| 9001 | System business error | Please contact technical support to troubleshoot the issue |
| 9007 | Non-integrator request | Please confirm if it is an integrator request |