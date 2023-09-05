**Brief Description:**

- Retrieves the URL of voice files for a user.

**Request Method:**
- URL: `http://api.nxcloud.com/api/voiceSms/getUserFileUrl`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter  | Required | Type   | Description                                                                 |
|:-----------|:---------|:-------|:----------------------------------------------------------------------------|
| account    | Yes      | string | Login username.                                                             |
| password   | Yes      | string | Password.                                                                   |
| page       | Yes      | int    | Current page.                                                               |
| page_size  | Yes      | int    | Number of items to display per page.                                         |
| startTime  | No       | string | Start time (yyyy-MM-dd).                                                    |
| endTime    | No       | string | End time (yyyy-MM-dd).                                                      |
| queryName  | No       | string | File name to query.                                                         |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/voiceSms/getUserFileUrl' \
--data-urlencode 'account=asdf' \
--data-urlencode 'password=qwer' \
--data-urlencode 'page=1' \
--data-urlencode 'page_size=10'
```

**Response Example:**

``` 
{
    "code": "success",
    "info": {
        "total": 3,
        "pageSize": 2,
        "page": 1,
        "rows": [
            {
                "gmt_create": "2019-05-28 20:05:32",
                "file_name": "录音 (1).mp3",
                "url": "https://nxcloudhk.oss-cn-hongkong.aliyuncs.com/voice_group/1559045130474.mp3"
            },
            {
                "gmt_create": "2019-05-28 20:04:32",
                "file_name": "录音 (2).mp3",
                "url": "https://nxcloudhk.oss-cn-hongkong.aliyuncs.com/voice_group/1559045070373.mp3"
            }
        ]
    }
}
```

**Response Parameter Description:**

| Parameter   | Type   | Description                                      |
|:------------|:-------|:-------------------------------------------------|
| gmt_create  | string | Creation time of the voice file.                  |
| file_name   | string | Name of the voice file.                           |
| url         | string | URL of the voice file.                            |

**Note:**

Failure parameters:

```
{
    "code": "failed",
    "info": "Please fill in the required parameters completely."
}
```

```
{
    "code": "failed",
    "info": "Please provide correct pagination parameters."
}
```

```
{
    "code": "failed",
    "info": "Incorrect account or password."
}
```