# Get Token

**Brief Description:**
Get the token for API calls. The token needs to be included in each API call. The default expiration time is 1200 seconds.

**Request URL:**
- `https://as01.nxcloud.com/v1/call/token`

**Request Method:**
- POST
- Content-Type: application/x-www-form-urlencoded

**Request Parameters:**

| Parameter   | Required | Type   | Description                                      |
|:------------|:---------|:-------|:-------------------------------------------------|
| appkey      | Yes      | string | Approval form appkey, obtained from the approval form list |
| secretkey   | Yes      | string | Approval form secretkey, obtained from the approval form list |

**Response Example:**
**Successful Response**
```
{"code":0,"token":"05804537D2A6693DC7E6CC5E0ADA09B9","expireinterval":1200}
```
**Failed Response**
```
{"code":1101,"info":"appkey or secretkey invalid."}
```

**Response Parameters:**

| Parameter      | Type   | Description                                      |
|:---------------|:-------|:-------------------------------------------------|
| code           | int    | Status ID: 0 for success, 1 for failure          |
| token          | string | Validation token                                 |
| expireinterval | int    | Expiration interval in seconds                    |
| info           | string | Failure description                              |

# Make Call

**Brief Description:**
Make a phone call using the nxcloud API.

**Request URL:**
- `https://as01.nxcloud.com/v1/call/makecall`

**Request Method:**
- POST
- Content-Type: application/x-www-form-urlencoded

**Request Parameters:**

| Parameter | Required | Type   | Description                                      |
|:----------|:---------|:-------|:-------------------------------------------------|
| token     | Yes      | string | Token obtained from the previous step             |
| username  | Yes      | string | Phone account                                    |
| phone     | Yes      | string | Called number                                    |
| showphone | No       | string | Phone number displayed on the recipient's device. Default: nxcloud |
| orderid   | No       | string | Order ID. Must be unique for each call. Length should be between 4 and 32, a combination of numbers and letters |

**Response Example:**
**Successful Response**
```
{
    "code": 0,
    "orderid": "xxx1234",
    "sessionid": "484ffc35-c59e-79c9-27a2-751cc1b52740",
    "info": "success"
}
```
**Failed Response**
```
{"code":1101,"info":"appkey or secretkey invalid."}
```

**Response Parameters:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | int    | Status ID: 0 for success, 1-10000 for failure    |
| info      | string | Failure description                              |

**Info Explanation:**

| Code  | Info                                            | Description                                      |
|:------|:------------------------------------------------|:-------------------------------------------------|
| 0     | success                                         | Success                                          |
| 1000  | data error, please reload token                  | Data error                                       |
| 1101  | appkey or secretkey invalid.                     | Invalid appkey or secretkey                      |
| 1201  | This token is not available                     | Token not available                              |
| 1201  | This token has expired                          | Token has expired                                |
| 1001  | Username no exist!                              | Phone account does not exist                     |
| 1002  | Username lock, please contact the administrator! | Phone account is locked                          |
| 1003  | User is not registered! please reload            | Phone account is not registered                  |
| 1004  | User is not registered! please reload            | Phone account is not registered                  |
| 1005  | User is not registered! please reload            | Phone account is not registered                  |
| 1006  | Username no exist                               | Phone account does not exist                     |
| 1007  | orderid format error                            | Invalid orderid format (only alphanumeric)       |
| 1008  | orderid length is too long                       | Orderid length is too long                        |
| 1100  | Data error!                                     | Data error                                       |
| 1200  | Parameter error!                                | Parameter error                                  |
| 10000 | unknown error                                   | Unknown error                                    |

***