## Interface Description: Query Current Number Binding Relationship List
### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter  | Type   | Required | Description                                                  |
| ---------- | ------ | -------- | ------------------------------------------------------------ |
| accessKey  | string | Yes      | User's accessKey                                             |
| action     | string | Yes      | Request method, e.g., getAXBList                             |
| bizType    | string | Yes      | Business type, fixed as 5, representing privacy number service |
| ts         | string | Yes      | Millisecond-level timestamp, e.g., 1670479632933             |
| sign       | string | Yes      | Signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Request Body

| Parameter | Type | Required | Description                                                  |
| --------- | ---- | -------- | ------------------------------------------------------------ |
| limit     | uint | Yes      | Value range [0, 1k], 0 means no limit (get all), maximum allowed is 1k data, regarding the issue of exceeding 1k when limit=0, only 1k data will be returned |
| offset    | uint | Yes      | Offset value, value range is [0, MAX], 0 means starting from the first record |

## Response Parameters

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | Return code, 0 means success, others mean failure |
| msg        | string | Return code description      |
| requestId  | string | Request ID                   |
| data       | Object | Request data                 |

Details of the **data** response parameters:

| Parameter  | Type     | Description                  |
| ---------- | -------- | ---------------------------- |
| bindList   | []Object | Return binding list          |
| total      | int      | Number of binding relationships returned |

Details of the parameters returned in **bind_list**:

| Parameter       | Type    | Description                                                  |
| --------------- | ------- | ------------------------------------------------------------ |
| customerId      | string  | Customer ID                                                  |
| businessId      | string  | Business ID (e.g., for taxi, express delivery, etc.)          |
| bindId          | string  | Binding ID returned by the privacy number service when binding |
| customerBindId  | string  | Customer-defined binding ID (determined by the customer, must be unique, either customerBindId or bindId can be used) |
| phoneA          | string  | Number A                                                     |
| phoneB          | string  | Number B, the country code of A and B must be consistent      |
| did             | string  | Bound virtual number of PNS                                  |
| flag            | int     | Other flags, bit combination, 0: none, 1: recording           |
| expireAt        | uint    | Expiration time in seconds, if 0, it means no expiration      |
| extension       | string  | Only used for extension number functionality                 |

## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### Header

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | xxxxxxxxxxxx                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | getAXBList                     |
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
    "bindList": [
      {
        "customerId": "cus_1",
        "businessId": "busi_1",
        "bindId": "b8c2aaf940d534d3c9ed8b780757f94e",
        "customerBindId": "1",
        "phoneA": "85211111114",
        "phoneB": "85222222222",
        "did": "85235753352",
        "flag": 0,
        "expireAt": 1670845212,
        "extension": "101"
      }
    ],
    "total": 1
  }
}
```