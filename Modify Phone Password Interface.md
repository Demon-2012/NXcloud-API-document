**Brief Description:**

- Interface for modifying phone passwords.

**Request Method:**
- URL: `https://api.nxcloud.com/api/sipphone/updatePassword`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter     | Required | Type   | Description                                                                 |
|:--------------|:---------|:-------|:----------------------------------------------------------------------------|
| appkey        | Yes      | string | App key for the approval application.                                        |
| secretkey     | Yes      | string | Secret key for the approval application.                                     |
| username      | Yes      | string | Phone username(s) to be modified. Multiple usernames can be passed.          |
| new_password  | No       | string | New password to be set. If not provided, a random password will be generated. If only one password is provided for multiple phones, all phones will have the same password. If multiple passwords are provided for multiple phones, ensure that the number of passwords matches the number of phones. |

**Request Example:**
```shell
curl --location --request POST 'https://api.nxcloud.com/api/sipphone/updatePassword' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'username=asdf'
```

**Response Example:**

```
{
    "code": "success",
    "row": {
        "1049001": "671897",
        "1049002": "888799"
    }
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | success or failed                                |
| row       | string | Phone username: Phone password                   |

**Note:**

- For more error codes, please refer to the error code description on the homepage.

{ "code": "failed", "info": "Your parameters are incorrect, please check and try again" }