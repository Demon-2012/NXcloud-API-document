## Summary

- Number Check Query Interface [Pagination]

### Request URL
`http://api2.nxcloud.com/api/number/query`

### Request Method
- Method: POST
- Content-Type: application/json

**Authentication Mechanism**

Please refer to the following link for authentication rules: [API Interface Calling Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

![image](https://user-images.githubusercontent.com/33716197/186609154-14abec1d-8e3f-41d0-91d6-d4d56c64fce7.png)

### Request Header

| Parameter Name | Parameter Type | Required | Example                     | Parameter Description                                      |
| :------------- | -------------- | -------- | --------------------------- | --------------------------------------------------------- |
| accessKey      | String         | Yes      | fme2na3kdi3ki               | User identity identifier                                  |
| ts             | String         | Yes      | 1655710885431               | Timestamp of the current request (in milliseconds). The maximum time difference allowed between the client and the NXCLOUD server is 60 seconds. |
| bizType        | String         | Yes      | 1                           | [Business Type] Fixed value used to identify number check  |
| action         | String         | Yes      | numbercheck                 | Fixed value used to identify number check                  |
| sign           | String         | Yes      | 6e9506557d1f289501d333ee2c365826 | API parameter signature, [Signature Algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Request Body

| Parameter Name | Required | Type    | Description                                                  |
| :------------- | :------- | :------ | ------------------------------------------------------------ |
| page           | Yes      | integer | Current page number                                          |
| pageSize       | Yes      | integer | Current page size, up to 100 records per page                |
| date           | Yes      | string  | Date in the format yyyy-MM-dd, can query up to 14 days of check records |
| messageId      | No       | string  | Message ID for querying check results, business ID, pushed in customer receipt [Exact search] |
| batchNo        | No       | string  | Batch number, batchNo and messageId cannot be empty at the same time [Batch search] |
| phone          | No       | string  | Phone number                                                 |
| appkey         | No       | string  | Application appkey                                           |
#### batchNo and messageId cannot be empty at the same time
#### Request Example

```json
{
    "batchNo": "101713775788",
    "page": 1,
    "date": "2023-08-12",
    "pageSize": 100
}
```

**Response Parameter Explanation**

| Parameter Name | Type    | Description                                                  |
| :------------- | :------ | ------------------------------------------------------------ |
| data           | object  | Request result, see details below                           |
| msg            | string  | Result description                                           |
| code           | integer | Result code                                                  |

**data**

| Parameter Name | Type    | Description                                                  |
| :------------- | :------ | ------------------------------------------------------------ |
| page           | integer | Current page number                                          |
| pageSize       | integer | Current page size                                            |
| totalPage      | integer | Total number of pages                                        |
| totalSize      | integer | Total number of records                                      |
| result         | array[object] | Check results, see details below                          |

**result**

| Parameter Name | Type    | Description                                                  |
| :------------- | :------ | ------------------------------------------------------------ |
| messageId      | string  | Message ID, maximum length of 64 characters                  |
| batchNo        | string  | Batch number                                                 |
| phone          | string  | Phone number                                                 |
| checkLevel     | integer | Check type: 1: Basic Version; 4: Call Version; 5: HLR Version |
| preCheck       | string  | Whether the format check passed. YES: Passed; NO: Not passed  |
| regionCode     | string  | Area code ISO                                                |
| countryCode    | string  | Country code                                                 |
| nationalNumber | string  | Local format                                                 |
| standNumber    | string  | Standard format                                              |
| numberType     | integer | Number type.<br>0: Other types<br>1: Fixed-line number<br>2: Mobile number<br>3: Toll-free number<br>4: VOIP number<br>5: Organization/Enterprise number<br>6: Special private number<br>7: Voicemail<br>8: Special restricted number |
| carrier        | string  | Carrier                                                      |
| price          | number  | Cost. Accurate to four decimal places                        |
| currency       | string  | Currency                                                     |

#### Additional Fields Returned for HLR Check
| Parameter Name | Type    | Description                                                  |
| :------------- | :------ | ------------------------------------------------------------ |
| validity       | string  | Whether the number is valid. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| reachable      | string  | Whether the device is reachable. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| roaming        | string  | Whether the number is roaming. "YES": Yes; "NO": No; "UNKNOWN": Unknown |

#### Additional Fields Returned for Call Version Check
| Parameter Name | Type    | Description                                                  |
| :------------- | :------ | ------------------------------------------------------------ |
| early          | string  | Whether it rings. "YES": Yes; "NO": No; "UNKNOWN": Unknown   |
| answered       | string  | Whether it is answered. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| response       | string  | Response status.<br>bell: Ringing<br>music: Ringback tone<br>busy: User busy<br>no_response: No response from user<br>invalid_number: Invalid number<br>not_available: Number not available<br>number_paused: Number paused<br>power_off: Power off<br>power_off_or_out_of_service: Power off or out of service area<br>voicemail: Voicemail<br>others: Temporarily unable to connect |

 
 **Successful Response 1**
```json 
{
    "msg": "Request successful",
    "code": 0,
    "data": {
        "result": [
            {
                "standNumber": "84****",
                "preCheck": "YES",
                "batchNo": "101713775788",
                "checkLevel": 2,
                "numberType": 2,
                "roaming": "",
                "messageId": "33f7c158a4194abe9ccdf3eac34a8422-2",
                "reachable": "",
                "regionCode": "VN",
                "carrier": "Viettel",
                "phone": "8498****",
                "nationalNumber": "98****",
                "countryCode": "84",
                "price": 0,
                "currency": "VND",
                "validity": ""
            },
            {
                "standNumber": "8498****",
                "preCheck": "YES",
                "batchNo": "101713775788",
                "checkLevel": 2,
                "numberType": 2,
                "roaming": "",
                "messageId": "33f7c158a4194abe9ccdf3eac34a8422-2",
                "reachable": "",
                "regionCode": "VN",
                "carrier": "Viettel",
                "phone": "849****",
                "nationalNumber": "98****",
                "countryCode": "84",
                "price": 0,
                "currency": "VND",
                "validity": ""
            }
        ],
        "totalSize": 2,
        "totalPage": 1,
        "pageSize": 100,
        "page": 1
    }
}
```

**Successful Response 2**
```json
{
    "msg": "Request successful",
    "code": 0,
    "data": {
        "totalSize": 0,
        "result": [],
        "totalPage": 0,
        "pageSize": 100,
        "page": 1
    }
}
```


 **Failed Response** 

```json
{
    "msg": "Incorrect date format [yyyy-MM-dd]",
    "code": 88,
    "data": {}
}
```

#### Error Codes

| code | msg|
| :--- | -------------------------------------------------- |
| 0    | Success                                               |
| 88   | Request failed with specific failure reason                        |
| 202| Application not available or incorrect appkey                                     |
| 210| Inconsistent customer information corresponding to the authentication mechanism and the customer information corresponding to the appkey                             |