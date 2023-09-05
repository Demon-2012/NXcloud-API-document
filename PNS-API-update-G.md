## API Documentation: Update Number Group

URL: https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter Name | Type   | Required | Description                                                  | Example        |
| -------------- | ------ | -------- | ------------------------------------------------------------ | -------------- |
| accessKey      | string | Yes      | User's accessKey                                             | fme2na3kdi3ki  |
| action         | string | Yes      | Request method                                               | updateGroup    |
| bizType        | string | Yes      | [Business Type] Fixed value to identify privacy number service | 5              |
| ts             | string | Yes      | Current request timestamp (in milliseconds). The maximum allowed time difference is 60 seconds | 1655710885431  |
| sign           | string | Yes      | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |                |

### Request Body

| Parameter Name | Required | Type   | Description                                                  |
| -------------- | -------- | ------ | ------------------------------------------------------------ |
| groupId        | Yes      | string | Number group ID                                              |
| operateType    | Yes      | uint   | Operation type for the G number group; 0: Add numbers, 1: Delete numbers, 2: Replace all numbers |
| phones         | Yes      | string | Phone numbers, separated by commas (,) for multiple numbers   |



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
| accessKey | sixgqophrnv4                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | updateGroup |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### Body

```json
{
    "groupId": "6a7sd3402px21429s04",
    "operateType": 1,
    "phones": "85211111114,85235753351,85235753311"
}
```

## Response Example

```json
{
  "code": 0,
  "msg": "success",
  "requestId": "1602248485121429504"
}
```