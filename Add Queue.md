**Brief Description:**

- Used to create a new queue and set basic queue information.

**Request URL:**
- `http://api.nxcloud.com/api/queue/sto_save`

**Request Method:**
- POST, submitted in HTTP FORM format.

**Parameters:**

| Parameter       | Required | Type   | Description                            |
|:----------------|:---------|:-------|:---------------------------------------|
| appkey          | Yes      | string | App key for the approval application.   |
| secretkey       | Yes      | string | Secret key for the approval application.|
| name            | Yes      | string | Queue name.                            |
| code            | Yes      | string | Country code.                          |
| mobile_names    | Yes      | string | Names of the phones to be added, separated by commas (,). |
| effective_number| Yes      | string | Display number.                         |
| phones          | Yes      | string | Numbers to be dialed, separated by commas (,). |
| callback_url    | No       | string | Data push address.                      |

**Response Example:**

``` 
{
    "callid": "104969",
    "queueid": "197",
    "code": "0",
    "info": "success"
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | 0 for success, others for failure.               |
| callid    | string | Access number.                                   |
| queueid   | string | Queue ID.                                        |

**Note:**
- N/A