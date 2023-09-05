**Brief Description:**

- API for converting long URLs to short links.

**Request Method:**
- URL: `http://api.nxcloud.com/api/shortLink/linkLong2Short`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter  | Required | Type   | Description                            |
|:-----------|:---------|:-------|:---------------------------------------|
| appkey     | Yes      | string | App key for the SMS application.        |
| secretkey  | Yes      | string | Secret key for the SMS application.     |
| url        | Yes      | string | Long URL (please use the original long URL). |
| remark     | No       | string | Remark.                                |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/shortLink/linkLong2Short' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'url=www.asdfghjklzxcvbnm.com'
```

**Response Example:**
``` 
{
    "code": "0",
    "info": "http://xxx/xxxxxx"
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | Result code.                                     |
| info      | string | Short link.                                      |

**Note:**

Error Codes

| Code | Description                                      |
|:-----|:-------------------------------------------------|
| 0    | Request succeeded.                               |
| 1    | Application is not available or key is incorrect. |
| 2    | Parameter error or empty.                        |
| 3    | Insufficient balance.                            |
| 9    | Illegal IP.                                      |
| 11   | Invalid email format.                            |
| 88   | Request failed.                                  |
| 99   | System error.                                    |
| 101  | Function is not enabled.                         |