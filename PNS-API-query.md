## API Documentation: Query the Other Bound Number Based on A, X or B, X

### Request URL
https://number.nxcloud.com/api/pns/

### Request Headers

| Parameter Name | Type   | Required | Description                                                  | Example        |
| -------------- | ------ | -------- | ------------------------------------------------------------ | -------------- |
| accessKey      | string | Yes      | User's accessKey                                             | fme2na3kdi3ki  |
| action         | string | Yes      | Request method                                               | queryAXB       |
| bizType        | string | Yes      | Business type, fixed as 5, representing privacy number service | 5              |
| ts             | string | Yes      | Millisecond-level timestamp                                   | 1655710885431  |
| sign           | string | Yes      | Signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |                |

### Request Body

| Parameter Name | Type   | Required | Description                                                  |
| -------------- | ------ | -------- | ------------------------------------------------------------ |
| caller         | string | Yes      | Calling number, country code is optional                      |
| did            | string | Yes      | DID number (intermediate number X), country code is required |



## Response Parameters

| Parameter Name | Type   | Description                        |
| -------------- | ------ | ---------------------------------- |
| code           | int    | Return code, 0 for success, others for failure |
| msg            | string | Return code description            |
| requestId      | string | Request ID                         |
| data           | Object | Returned data                      |

The structure of the data object is as follows:

| Parameter Name      | Type   | Description                                                  |
| ------------------- | ------ | ------------------------------------------------------------ |
| callee              | string | Called number                                                |
| callId              | string | Call ID                                                      |
| flag                | uint   | Other flags, bitwise combination, 0: none, 1: recording       |
| audioWhenCallFail   | string | If ret_code != 0 and audio_when_call_fail is not empty, play this audio file in WAV format |
| bindType | uint | Used for extension number function. When it returns 4, it means binding for extension number |
| audioWhenDtmfNeed   | string | If the user needs to enter an extension, play this audio file in WAV format |
| audioWhenDtmfErr    | string | If the extension number input is incorrect, play this audio file in WAV format |


## Request Example

### Request URL
https://number.nxcloud.com/api/pns/

### **Header**

| KEY       | VALUE                            |
| --------- | -------------------------------- |
| accessKey | xxxxxxxxxxxx                     |
| ts        | 1670479632933                    |
| bizType   | 5                                |
| action    | queryAXB                         |
| sign      | faxxxxxxxxxxxxxxxxxxxxxxxxxxxxd4 |

### **Body**

```json
{
    "caller": "85222222222",
    "did": "85235753352"
}
```

## Response Example

```json
{
    "code": 0,
    "msg": "success",
    "requestId": "1602233475628404736",
    "data": {
        "callee": "85211111114",
        "callId": "1602233475636793344",
        "flag": 0,
        "audioWhenCallFail": "",
        "bindType": 4,
        "audioWhenDtmfErr": "",
        "audioWhenDtmfNeed": ""
    }
}
```