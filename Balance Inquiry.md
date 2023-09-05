**Brief Description:**

- Get customer balance.

**Request Method:**
- URL: `http://api.nxcloud.com/api/common/getBalance`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter  | Required | Type   | Description                          |
|:-----------|:---------|:-------|:-------------------------------------|
| appkey     | Yes      | string | Any enabled SMS application appkey    |
| secretkey  | Yes      | string | Any enabled SMS application secretkey |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/common/getBalance' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer'
```

**Response Example:**

``` 
{"code": "0","balance": "3788.32", "credit_balance":"500"}
```

**Response Parameter Description:**

| Parameter       | Type   | Description       |
|:----------------|:-------|:------------------|
| code            | string | Result code       |
| balance         | string | Balance           |
| credit_balance  | string | Credit balance    |

**Note:**

- Error Codes

| code | Description     |
|:-----|:----------------|
| 0    | Request success |