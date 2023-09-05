## Interface Description: Query Number Groups
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter  | Type   | Required | Description                                                  | Example       |
| ---------- | ------ | -------- | ------------------------------------------------------------ | ------------- |
| accessKey  | string | Yes      | User's accessKey                                             | fme2na3kdi3ki |
| action     | string | Yes      | Request method                                               | listGroup |
| bizType    | string | Yes      | [Business type] Fixed value to identify privacy number service | 5             |
| ts         | string | Yes      | Timestamp of the current request (in milliseconds). The maximum time difference allowed between the client and the server is 60 seconds. | 1655710885431 |
| sign       | string | Yes      | API parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |               |

### Request Body

| Parameter | Required | Type | Description                                                  |
| --------- | -------- | ---- | ------------------------------------------------------------ |
| limit     | Yes      | uint | Value range [0, 1k], 0 means no limit (get all), maximum allowed is 1k data, regarding the issue of exceeding 1k when limit=0, only 1k data will be returned |
| offset    | Yes      | uint | Offset value, value range is [0, MAX], 0 means starting from the first record |

## Response Parameters

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | Return code, 0 means success, others mean failure |
| msg        | string | Return code description      |
| requestId  | string | Request ID                   |
| data       | Object | Return data                  |

Details of the parameters returned in **data**:

| Parameter  | Type     | Description                  |
| ---------- | -------- | ---------------------------- |
| groups     | []Object | Number groups                |
| total      | int      | Number of number groups       |

Details of the parameters returned in **groups**:

| Parameter   | Type   | Description                                                  |
| ----------- | ------ | ------------------------------------------------------------ |
| customerId  | string | Customer ID                                                  |
| groupName   | string | Name of the G number group                                   |
| groupId     | string | G number group ID                                            |
| phones      | string | Phone numbers, multiple numbers separated by commas (,)      |
| remark      | string | Remarks of the G number group                                |



## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### Header

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | sixgqophrnv4                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | listGroup |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### Body

```json
{
    "limit":10,
    "offset":0
}
```

## Response Example

```json
{
  "code": 0,
  "msg": "success",
  "requestId": "1602262837283131392",
  "data": {
    "groups": [
      {
        "customerId": "cus_1",
        "groupName": "groupA",
        "groupId": "b8c2aaf940d534d3c9ed8b780757f94e",
        "phones": "85211111114,85235753351,85235753311",
        "remark": "Number Group A"
      }
    ],
    "total": 1
  }
}
```