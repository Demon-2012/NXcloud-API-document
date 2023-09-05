**Brief Description:**

- Email verification code record query.

**Request Method:**
- URL: `http://api2.nxcloud.com/api/email/dr`
- Method: `POST`
- Content-Type: `application/json`

**Parameters:**
###### **Headers:**
| Parameter     | Value              | Required | Type   | Description |
|:--------------|:-------------------|:---------|:-------|:------------|
| Content-Type  | application/json   | Yes      |        |             |

###### **Body:**
| Parameter   | Type   | Required | Description                           |
|:------------|:-------|:---------|:--------------------------------------|
| appKey      | string | Yes      | Email application appKey               |
| secretKey   | string | Yes      | Email application secretKey            |
| messageId   | string | No       | Email ID                              |
| startTime   | string | No       | Start time (yyyy-MM-dd HH:mm:ss)       |
| endTime     | string | No       | End time (yyyy-MM-dd HH:mm:ss)         |
| current     | number | No       | Page number, default is 1              |
| size        | number | No       | Number of items per page, default is 10, maximum is 100 |

**Request Example:**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/email/dr' \
--header 'Content-Type: application/json' \
--data-raw '{
    "appKey": "asdf",
    "secretKey": "qwer"
}'
```

**Response Example:**

``` 
{
    "msg": "success",
    "result": {
        "records": [
            {
                "messageId": "7128fd39195d4e2faf85de7f054514e6",
                "customerName": "NX00777-customer",
                "appName": "name2",
                "tplSubject": "123222",
                "sender": "1990336062@qq.com",
                "receiver": "ye.aoxiang@nxtele.com",
                "sellPrice": 0.26500000,
                "sendTime": "2021-02-23T15:39:51",
                "msgResult": "DELIVRD"
            }
        ],
        "total": 1,
        "size": 10,
        "current": 1,
        "orders": [],
        "appKey": "appKey",
        "secretKey": "secretKey",
        "messageId": "7128fd39195d4e2faf85de7f054514e6",
        "startTime": null,
        "endTime": null,
        "sortType": 0,
        "searchCount": true,
        "pages": 1
    },
    "code": 200
}
```

**Response Parameter Description:**

| Parameter     | Type   | Description                                      |
|:--------------|:-------|:-------------------------------------------------|
| msg           | string | Response message                                 |
| result        | object | Request result                                   |
| records       | object |                                                  |
| messageId     | string | Email ID                                         |
| customerName  | string | Name                                             |
| appName       | string | Application name                                 |
| tplSubject    | string | Template name                                    |
| sender        | string | Sender's email                                   |
| receiver      | string | Receiver's email                                 |
| sellPrice     | string | Unit price                                       |
| sendTime      | string | Sending time                                     |
| msgResult     | string | Message result                                   |
| total         | string | Total number of records                          |
| size          | string | Number of items per page                         |
| current       | string | Current page                                     |
| appKey        | string | Email application appKey                         |
| secretKey     | string | Email application secretKey                      |
| messageId     | string | Email ID                                         |
| startTime     | string | Start time (yyyy-MM-dd HH:mm:ss)                  |
| endTime       | string | End time (yyyy-MM-dd HH:mm:ss)                    |
| sortType      | string | Sorting type: default is descending              |
| code          | string | Response code                                    |

**Error Codes:**

| Code    | Description                                      |
|:--------|:-------------------------------------------------|
| 0       | Request successful                               |
| 601001  | Account status exception                         |
| 601002  | Insufficient account balance                     |
| 601101  | Application status exception, appKey/SecretKey mismatch |
| 601102  | No pricing available for the application         |
| 601103  | No domain configuration under the application    |
| 601104  | Domain not verified                              |
| 601105  | Sender's email address does not exist            |
| 601106  | Email template does not exist                    |
| 601107  | Email template not approved                      |
| 601201  | Submission failed                                |