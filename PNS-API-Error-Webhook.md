## Summary

- When making a call without an existing binding relationship, the call will fail, and the error call information will be pushed to the specified URL.

## URL Configuration

- Configuration is done by providing a URL to the development team.

## Request Method

- Method: POST
- Content-Type: application/json

### Retry Rules

In general, call detail records will be pushed to the specified address after the call ends. Receiving an HTTP 200 OK means that the receipt push has been accepted, and the request is considered completed. If an HTTP ERROR message is received, NXCLOUD will retry the push every minute for up to 60 minutes until it succeeds. If it still fails after 60 minutes, no further retries will be made.

## **Push Field Description**

| Parameter  | Type   | Description                  |
| ---------- | ------ | ---------------------------- |
| code       | int    | Return code, 0 means success, others mean failure |
| msg        | string | Return code description      |
| requestId  | string | Request ID                   |
| data       | struct | Data                         |

Parameters in **data** are as follows:

| Parameter         | Type   | Description                  |
| ----------------- | ------ | ---------------------------- |
| action            | string | Request interface            |
| requestParams     | struct | Request parameters           |
| occurrenceTime    | string | Request time                 |

Parameters in **requestParams** are as follows:

| Parameter  | Type   | Description                  |
| -----------| ------ | ---------------------------- |
| caller      | string | Calling number               |
| did         | string | DID number (intermediate number X) |



## Push Demo

```json
{
  "code": 10013,
  "msg": "binding not exist",
  "requestId": "1640920940635361280",
  "data": {
    "action": "queryAXB",
    "requestParams": {
      "caller": "852121199",
      "did": "85299999999"
    },
    "occurrenceTime": "2023-03-29 11:36:53"
  }
}
```