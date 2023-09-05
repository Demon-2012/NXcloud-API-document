## API Documentation: Create Number Group

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter  | Type   | Required | Description                                                  | Example       |
| ---------- | ------ | -------- | ------------------------------------------------------------ | ------------- |
| accessKey  | string | Yes      | User's accessKey                                             | fme2na3kdi3ki |
| action     | string | Yes      | Request method                                               | createGroup   |
| bizType    | string | Yes      | [Business type] Fixed value to identify privacy number service | 5             |
| ts         | string | Yes      | Current timestamp of the request (in milliseconds). The maximum time difference allowed between the client and the server is 60 seconds. | 1655710885431 |
| sign       | string | Yes      | Signature of the API input parameters. [Signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |               |

### Request Body

| Parameter  | Required | Type   | Description                                                  |
| ---------- | -------- | ------ | ------------------------------------------------------------ |
| phones     | Yes      | string | Phone numbers to be added to the newly created group. Multiple numbers should be separated by commas (,) and include the country code. |
| groupName  | No       | string | Name of the G number group. If empty, the name will be the same as the groupId. |
| remark     | No       | string | Remark information for the G number group.                    |



## Response Parameters

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | Return code, 0 means success, others mean failure |
| msg        | string | Return code description      |
| requestId  | string | Request ID                   |
| groupId    | string | ID of the newly created number group |

## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | sixgqophrnv4                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | createGroup                      |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### Request Body

```json
{
    "phones": "85211111114,85235753351,85235753311",
    "groupName": "groupA",
    "remark": "Number Group A"
}
```

## Response Example

```json
{
  "code": 0,
  "msg": "success",
  "requestId": "1602248485121429504",
  "groupId": "6a7sd3402px21429s04"
}
```