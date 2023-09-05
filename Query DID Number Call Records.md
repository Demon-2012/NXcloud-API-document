**DID Number Call Record Query**

- URL: `https://api2.nxcloud.com/api/did/cdr`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

<br>

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

<br>

## Request Parameters
### Header Parameters:

| Parameter Name | Type    | Required | Example            | Description                   |
| -------------- | ------- | -------- | ------------------ | ----------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki      | User identity identifier      |
| ts             | String  | Yes      | 1655710885431      | Timestamp of the current request in milliseconds. The maximum time difference allowed between the user and the server is 60 seconds |
| bizType        | String  | Yes      | 4                  | Business type, fixed value "4" |
| action         | String  | Yes      | cdr                | Business operation, fixed value "cdr" |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example      | Description                                                  |
| -------------- | ------ | -------- | ------------ | ------------------------------------------------------------ |
| date           | string | Yes      | 2022-10-01   | Date (yyyy-MM-dd)                                            |
| pageSize       | integer| Yes      | 10           | Number of records per page (less than 1000)                  |
| page           | integer| Yes      | 1            | Starting page                                                |
| didNumber      | string | No       | 123456789    | DID number. If empty, there is no restriction on the DID number |
| callNumber     | string | No       | 123456789    | Call number. If empty, there is no restriction on the call number |
| type           | integer| No       | 0            | Call type: 0 for incoming, 1 for outgoing. If empty, there is no restriction on the call type |

<br>

## Request Example

```json
{
    "type": 0,
    "date": "2022-08-23",
    "pageSize": 10,
    "page": 1
}
```


<br>

## Response Parameters

| Parameter Name | Type       | Description       |
| -------------- | ---------- | ----------------- |
| code           | Integer    | Result code       |
| data           | JsonObject | Request result    |
| message        | String     | Request explanation |

- data Object parameters:

| Parameter Name | Type       | Description       |
| -------------- | ---------- | ----------------- |
| totalRow       | Integer    | Total number of data rows |
| pageNumber     | Integer    | Current page number |
| totalPage      | Integer    | Total number of data pages |
| pageSize       | Integer    | Number of records per page |
| list           | array of items | Current page result list |

- list item parameters:

| Parameter Name   | Type       | Description       |
| ---------------- | ---------- | ----------------- |
| number           | string     | DID number        |
| callNumber       | string     | Call number       |
| callType         | int        | Call type: 0 for incoming, 1 for outgoing |
| countryName      | string     | Country direction |
| callDuration     | long       | Call duration (in seconds) |
| feeType          | int        | Billing method: 0: 60+60, 1: 1+1 |
| feeDurationMinute| bigDecimal | Billing duration (in minutes) |
| callPriceUnit    | bigDecimal | Call unit price (in yuan) |
| callPrice        | bigDecimal | Call cost (in yuan) |
| endDirection     | int        | Hang-up direction: 0 for caller, 1 for callee, other: other |
| endReason        | string     | Termination reason code |
| endReasonName    | string     | Termination reason |
| callerIp         | string     | Caller IP |
| calleeIp         | string     | Callee IP |
| startTime        | string     | Call start time |
| endTime          | string     | Call end time |

<br>

## Response Example

### Successful Example

```json
{
    "code": 0,
    "data": {
        "totalRow": 1,
        "pageNumber": 1,
        "totalPage": 1,
        "pageSize": 10,
        "list": [
            {
                "callDuration": 64,
                "endReason": "-7",
                "feeDurationMinute": 2,
                "feeType": 0,
                "callType": 0,
                "callerIp": "127.0.0.1",
                "endReasonName": "Caller Hang-up",
                "callNumber": "123456789",
                "calleeIp": "127.0.0.1",
                "callPrice": 0.11,
                "endDirection": 0,
                "startTime": "2022-10-01 11:04:57",
                "id": 1,
                "countryName": "Thailand",
                "endTime": "2022-10-01 11:06:01",
                "callPriceUnit": 0.055
            }
        ]
    },
    "message": "Request successful"
}
```

### Failed Example

```json
{
    "code": 1002,
    "data": null,
    "message": "Parameter error"
}
```

<br>

## Response Code Explanation

| code      | message      | Solution                   |
| --------- | ------------ | -------------------------- |
| 0         | Request successful     |                            |
| -1        | Request failed     | Please contact technical support to troubleshoot the issue     |
|1002		| Parameter error     | Parameter exception, please check the required parameters      |
| 1000~100X | Authentication issue     | Refer to the API authentication section for details        |