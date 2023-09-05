# Login Verification Status Callback

Push the login verification status.

**Request URL:**
- The HTTP interface address for DR push (provided by the user)
- Example: `http://106.15.34.94:8989/ota/callback`

**Request Method:**
- POST
- Related parameters are passed in the URL as query strings.

**Parameters:**

| Parameter | Required | Type   | Description                                      |
| --------- | -------- | ------ | ------------------------------------------------ |
| requestId | Yes      | string | The requestId obtained from the one-click login request |
| phone     | Yes      | string | Phone number                                     |
| status    | Yes      | string | Identity verification result (SUCCESS: success, PENDING: waiting, MISMATCH: mismatch, FAILURE: failure, UNKNOWN: unknown) |
| drTime    | Yes      | string | Report time in the format: yyyy-MM-dd HH:mm:ss   |

**Callback Example**

```
http://106.15.34.94:8080/ota/callback?phone=6282167624806&requestId=b308d94a73f94e6d84ae975c41f4b2a6&drtime=2021-02-26 10:01:15&status=SUCCESS
```

**User Response**
- Return "success" for success.
- Return "error" for failure.