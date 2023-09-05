## API Documentation: Unbind A and B Based on bindId

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| accessKey      | string | Yes      | User's accessKey                                             |
| action         | string | Yes      | Request method, example: unbindAXB                           |
| bizType        | string | Yes      | Business type, fixed as 5, representing privacy number service |
| ts             | string | Yes      | Millisecond-level timestamp, example: 1670479632933          |
| sign           | string | Yes      | Signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Request Body

| Parameter Name   | Type   | Required | Description                                                  |
| ---------------- | ------ | -------- | ------------------------------------------------------------ |
| customerBindId   | string | No       | Customer-defined bind ID (determined by the customer, must be unique). Either customerBindId or bindId is required. |
| bindId           | string | No       | Bind ID returned by the privacy number service during binding. Either customerBindId or bindId is required. |



## Response Parameters

| Parameter Name | Type   | Description                        |
| -------------- | ------ | ---------------------------------- |
| code           | int    | Return code, 0 for success, others for failure |
| msg            | string | Return code description            |
| requestId      | string | Request ID                         |



## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### Header

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | xxxxxxxxxxxx                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | unbindAXB                       |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### Body

```json
{
    "bindId": "f6e24ebdaf64ef91adb0b60e3b582db0"
}
```

## Response Example

```json
{
    "code": 0,
    "msg": "success",
    "requestId": "1602135125931462656"
}
```