

**Brief Description:**

- ~~Call Status Callback Push Interface V1.0~~ (This interface is temporarily unavailable)

**Push Request URL:**
- Customer development receiving interface for callback push

**Push Request Method:**
- POST

**Parameters:**

| Parameter | Required | Type   | Description              |
|:----------|:---------|:-------|:-------------------------|
| sessionid | Yes      | string | Unique ID                |
| state     | Yes      | int    | Call state: 1: Start calling; 2: Connected; 3: In call; 4: Hang up |
| time      | Yes      | string | Time (Unix timestamp)    |
| info      | Yes      | string | Return information       |

**Push JSON Parameter Example:**

```
{
    "sessionid": "fe5f20eb-b054-4c52-8784-636d5d626c2f",
    "state": 1,
    "time": "1552628370.54565",
    "info": "start calling"
}
```

**Note:**
- This interface is currently unavailable.