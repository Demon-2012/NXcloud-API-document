**Brief Description:**

- Email verification code delivery receipt (DR) callback.

**Request URL:**
- HTTP interface address for DR callback (provided by the user).
- Example: `http://106.15.34.94:8989/email/callback`

**Request Method:**
- POST

**Parameters:**
###### **Headers:**
| Parameter     | Value              | Required | Type   | Description |
|:--------------|:-------------------|:---------|:-------|:------------|
| Content-Type  | application/json   | Yes      |        |             |

###### **Body:**
| Parameter  | Type   | Required | Description              |
|:-----------|:-------|:---------|:-------------------------|
| messageId  | string | Yes      | Email ID                 |
| sender     | string | Yes      | Sender's email           |
| receiver   | array  | Yes      | Receiver's email(s)      |
| price      | string | Yes      | Unit price               |
| result     | string | Yes      | Status: DELIVRD/UNDELIV  |
| sendTime   | string | Yes      | yyyy-MM-dd HH:mm:ss      |

**Response Parameter Description:**

| Parameter | Type   | Required | Description |
|:----------|:-------|:---------|:------------|
|           | string | No       | success/failure |

