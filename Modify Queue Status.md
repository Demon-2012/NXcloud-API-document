**Brief Description:**

- Used to modify the state of a queue.

**Request URL:**
- `http://api.nxcloud.com/api/queue/state`

**Request Method:**
- POST

**Parameters:**

| Parameter | Required | Type   | Description                            |
|:----------|:---------|:-------|:---------------------------------------|
| appkey    | Yes      | string | App key for the approval application.   |
| secretkey | Yes      | string | Secret key for the approval application.|
| queueid   | Yes      | string | Queue ID.                              |
| state     | Yes      | string | State value.                           |

**Response Example:**

``` 
{
    "code": "0",
    "state": "1",
    "info": "success"
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | 0 for success, others for failure.               |
| state     | string | State value: 0 - Not called, 1 - Start calling, 2 - Pause, 3 - Marked as completed, 4 - Marked as canceled. |

**Note:**
- N/A