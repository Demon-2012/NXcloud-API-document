**Brief Description:**

- Used to modify basic information of a queue.

**Request URL:**
- `http://api.nxcloud.com/api/queue/sto_update`

**Request Method:**
- POST, submitted in HTTP FORM format.

**Parameters:**

| Parameter       | Required | Type   | Description                            |
|:----------------|:---------|:-------|:---------------------------------------|
| appkey          | Yes      | string | App key for the approval application.   |
| secretkey       | Yes      | string | Secret key for the approval application.|
| queueid         | Yes      | string | Queue ID.                              |
| name            | Yes      | string | Queue name.                            |
| mobile_names    | Yes      | string | Phones to be changed, separated by commas (,). |
| effective_number| Yes      | string | Display number.                         |

**Response Example:**

``` 
{
    "code": "0",
    "info": "success"
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | 0 for success, others for failure.               |

**Note:**
- N/A