**Brief Description:**
- Used to manage the call status of a phone. It can either hang up the phone directly or only hang up the current call.

**Request URL:**
- `http://api.nxcloud.com/api/queue/kill`

**Request Method:**
- POST

**Parameters:**

| Parameter  | Required | Type   | Description              |
|:-----------|:---------|:-------|:-------------------------|
| appkey     | Yes      | string | App key for the approval |
| secretkey  | Yes      | string | Secret key for the approval |
| sessionid  | Yes      | string | Agent ID or UUID from the callback |

**Response Example:**

```json
{
    "code": "0",
    "info": "success"
}
```

**Response Parameters:**

| Parameter | Type   | Description                          |
|:----------|:-------|:-------------------------------------|
| code      | string | "0" indicates success, others indicate failure |

**Note:**
- When the sessionid is the agent ID, it will hang up the agent's phone.
- When the sessionid is the UUID from the callback, it will hang up the ongoing call with the callee, while the agent remains online.