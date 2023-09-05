**Brief Description:**

- Voice verification code reporting interface.

**Request URL:**
- `http://api2.nxcloud.com/api/voiceSms/conversion`

**Request Method:**
- POST
- Content-Type: application/json

**Request Example:**
```
POST http://api2.nxcloud.com/api/voiceSms/conversion
Content-Type: application/json

{
    "messageid": "7c9f36842095480189603142a4df76ed",
    "status": 1
}
```

**Request Parameters:**

| Parameter  | Required | Type    | Description                                      |
|:-----------|:---------|:--------|:-------------------------------------------------|
| messageid  | Yes      | String  | Voice ID returned when submitting the voice verification code |
| status     | Yes      | Integer | 1 for successful reporting, 0 for not reported   |

**Response Example:**
- Success response example: `{"code": "success","info": "success"}`
- Failure response example: `{"code": "failed","info": "messageid not exist"}`

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | String | Result code. "success" for success, "failed" for failure |
| info      | String | Request result prompt message                     |