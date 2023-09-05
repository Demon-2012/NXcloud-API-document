## Summary

- Number Check Result Push

### Request URL
- Specified through the `drUrl` field in the [Submit Check](https://github.com/nxtele/http-api-document/wiki/Number-Check-API-submit) API or configured on the NXCLOUD platform.

### Request Method
- Method: POST
- Content-Type: application/json

### Retry Rules
In general, the check result will be pushed back to the specified API address within 10 seconds to 5 minutes. Receiving an HTTP 200 OK indicates that NXCLOUD has accepted the receipt push, and NXCLOUD considers the request completed.
If an HTTP ERROR message is received, NXCLOUD will retry the push every minute for up to 60 minutes until it succeeds. If it still fails after 60 minutes, no further retries will be made.

#### Request Body

**Basic Version**
```json
{
    "messageId": "83ac9512-3c47-495d-a3c4-6d77a9f1149c",
    "code": 0,
    "msg": "success",
    "batchNo": "700337042751",
    "phone": "234800001xxxxx",
    "data": {
        "basic": {
            "preCheck": "YES",
            "regionCode": "CN",
            "countryCode": "86",
            "nationalNumber": "800001xxxxx",
            "standNumber": "234800001xxxxx",
            "numberType": 2,
            "carrier": "China Telecom"
        }
    },
    "cost": {
        "price": 0.1912,
        "currency": "USD"
    }
}
```

**HLR Check**
```json
{
    "messageId": "83ac9512-3c47-495d-a3c4-6d77a9f1149c",
    "code": 0,
    "msg": "success",
    "batchNo": "700337042751",
    "phone":"234800001xxxxx",
    "data": {
        "basic": {
            "preCheck": "YES",
            "regionCode": "CN",
            "countryCode": "86",
            "nationalNumber": "800001xxxxx",
            "standNumber": "234800001xxxxx",
            "numberType": 2,
            "carrier": "China Telecom"
        },
        "live": {
            "validity": "YES",
            "reachable": "UNKNOWN",
            "roaming": "UNKNOWN"
        }
    },
    "cost": {
        "price": 0.9230,
        "currency": "USD"
    }
}

```

**Call Version**
```json
{
    "messageId": "83ac9512-3c47-495d-a3c4-6d77a9f1149c",
    "code": 0,
    "msg": "success",
    "batchNo": "700337042751",
    "phone": "234800001xxxxx",
    "data": {
        "basic": {
            "preCheck": "YES",
            "regionCode": "CN",
            "countryCode": "86",
            "nationalNumber": "800001xxxxx",
            "standNumber": "234800001xxxxx",
            "numberType": 2,
            "carrier": "China Telecom"
        },
        "dial": {
            "early": "NO",
            "answered": "NO",
            "response": "invalid_number"
        }
    },
    "cost": {
        "price": 1.0231,
        "currency": "USD"
    }
}
```

**Check Failure**
```json
{
    "messageId": "cc5ef7d6-62be-42c9-abdf-b6ea9d6ed5e6",
    "code": 114,
    "msg": "Invalid number format",
    "batchNo": "700337042751",
    "phone":"18617"
}
```

**Receipt Result Explanation**

| Parameter   | Type    | Description                                                  |
| :---------- | :------ | ------------------------------------------------------------ |
| messageId   | string  | Message ID, maximum length of 64 characters                  |
| code        | integer | code=0 indicates success                                     |
| msg         | string  | Result description                                           |
| batchNo     | string  | Batch number                                                 |
| phone       | string  | Phone number                                                 |
| basic       | object  | Basic version information, see details below                  |
| live        | object  | Advanced version information, see details below               |
| dial        | object  | Call version information, see details below                   |
| cost        | object  | Cost information, see details below                           |


**basic**

| Parameter       | Type    | Description                                                  |
| :-------------- | :------ | ------------------------------------------------------------ |
| preCheck        | string  | Whether the format check passed. YES: Passed; NO: Not passed  |
| regionCode      | string  | Area code ISO                                                |
| countryCode     | string  | Country code                                                 |
| nationalNumber  | string  | Local format                                                 |
| standNumber     | string  | Standard format                                              |
| numberType      | integer | Number type.<br>0: Other types<br>1: Fixed-line number<br>2: Mobile number<br>3: Toll-free number<br>4: VOIP number<br>5: Organization/Enterprise number<br>6: Special private number<br>7: Voicemail<br>8: Special restricted number |
| carrier         | string  | Carrier                                                      |

**live**

| Parameter       | Type    | Description                                                  |
| :-------------- | :------ | ------------------------------------------------------------ |
| validity        | string  | Whether the number is valid. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| reachable       | string  | Whether the device is reachable. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| roaming         | string  | Whether the number is roaming. "YES": Yes; "NO": No; "UNKNOWN": Unknown |

**dial**

| Parameter       | Type    | Description                                                  |
| :-------------- | :------ | ------------------------------------------------------------ |
| early           | string  | Whether it rings. "YES": Yes; "NO": No; "UNKNOWN": Unknown   |
| answered        | string  | Whether it is answered. "YES": Yes; "NO": No; "UNKNOWN": Unknown |
| response        | string  | Response status.<br>bell: Ringing<br>music: Ringback tone<br>busy: User busy<br>no_response: No response from user<br>invalid_number: Invalid number<br>not_available: Number not available<br>number_paused: Number paused<br>power_off: Power off<br>power_off_or_out_of_service: Power off or out of service area<br>voicemail: Voicemail<br>others: Temporarily unable to connect |

**cost**

| Parameter       | Type    | Description                                                  |
| :-------------- | :------ | ------------------------------------------------------------ |
| price           | number  | Cost. Accurate to four decimal places                        |
| currency        | string  | Currency                                                     |

**Receipt Error Codes**

| code | msg              |
| :--- | -------------------- |
| 0    | Success              |
| 103  | Internal server error       |
| 108  | Invalid value in the request       |
| 112  | Backend service call failed     |
| 114  | Invalid number format         |
| 120  | Non-mobile number check not supported |
| 121  | Unknown error             |
| 122  | Information not detected       |