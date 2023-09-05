## API Documentation: Bind A and B Numbers and Return X Number

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter  | Type   | Required | Description                                                  | Example       |
| ---------- | ------ | -------- | ------------------------------------------------------------ | ------------- |
| accessKey  | string | Yes      | User's accessKey                                             | fme2na3kdi3ki |
| action     | string | Yes      | Request method                                               | bindAXB       |
| bizType    | string | Yes      | [Business type] Fixed value to identify privacy number service | 5             |
| ts         | string | Yes      | Current timestamp of the request (in milliseconds). The maximum time difference allowed between the client and the server is 60 seconds. | 1655710885431 |
| sign       | string | Yes      | Signature of the API input parameters. [Signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |               |

### Request Body

| Parameter       | Required | Type   | Description                                                  |
| ---------------- | -------- | ------ | ------------------------------------------------------------ |
| phoneA           | Yes      | string | Number A, the country code of A and B numbers must be the same |
| phoneB           | Yes      | string | Number B, the country code of A and B numbers must be the same |
| customerBindId   | No       | string | Custom binding ID (determined by the customer, must be unique), can be empty |
| flag             | No       | int    | Other flags, bit combination, 0: none, 1: recording          |
| expireSecond     | Yes      | int    | Expiration time in seconds, if 0, it means no expiration     |



## Response Parameters

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | Return code, 0 means success, others mean failure |
| msg        | string | Return code description      |
| requestId  | string | Request ID                   |
| data       | Object | Request data ID              |

Details of the data returned by the `data` parameter:

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| bindId     | string | Binding ID of PNS, subsequent billing will be based on this |
| did        | string | Virtual number bound by PNS   |



## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | sixgqophrnv4                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | bindAXB                          |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### Request Body

```json
{
    "phoneA": "85211111114",
    "phoneB": "85222222222",
    "customerBindId": "1",
    "expireSecond": 1011
}
```

## Response Example

```json
{
  "code": 0,
  "msg": "success",
  "requestId": "1602248485121429504",
  "data": {
    "bindId": "f6e24ebdaf64ef91adb0b60e3b582db0",
    "did": "85235753351"
  }
}
```