**Brief Description:**

- Voice group call/notification/verification record query.
- Note: The cost calculation in the voice call records has a certain delay. If you need accurate cost information, please integrate the receipt push interface.

**Request Method:**
- URL: `http://api2.nxcloud.com/api/voiceSms/getVoiceCdr`
- Method: `POST` (Do not pass the body, submit using form data)
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter   | Required | Type   | Description                                      |
|:------------|:---------|:-------|:-------------------------------------------------|
| appkey      | Yes      | string | Voice application appkey                         |
| secretkey   | Yes      | string | Voice application secretkey                      |
| voiceType   | Yes      | string | Voice service type: 0 for group call, 1 for verification/notification |
| messageid   | No       | string | messageid                                        |
| start_time  | Yes      | string | Start time (Format: yyyy-MM-dd HH:mm:ss)         |
| end_time    | Yes      | string | End time (Format: yyyy-MM-dd HH:mm:ss)           |
| page_size   | Yes      | string | Number of items per page                         |
| page        | Yes      | string | Current page (starting from 1)                   |

**Request Example:**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/voiceSms/getVoiceCdr' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'voiceType=1' \
--data-urlencode 'messageid=32432423' \
--data-urlencode 'start_time=2019-09-09 09:00:01' \
--data-urlencode 'end_time=2019-09-09 09:00:11' \
--data-urlencode 'page_size=10' \
--data-urlencode 'page=1'
```

**Response Example:**
*1. Voice group call*
```json
{
    "code": "1",
    "info": {
        "total": 1,
        "page": 1,
        "pageSize": 5,
        "rows": [
            {
                "id": 11112,
                "result": "Successful connection",
                "cycle": 20,
                "time": "2019-09-09 09:00:00",
		"start_time": "2019-09-09 09:00:01",
		"end_time": "2019-09-09 09:00:20",
                "phone": "810022458",
                "basic_price": 0.005,
                "second": 19,
                "countryCode": "91",
                "messageid": 784522,
                "customer_price": 0.05,
                "show_phone": "085944247",
                "size": 1,
		"ivr_result":1
            }
        ]
    }
}
```

*2. Voice verification/notification*
```json
{
    "code": "1",
    "info": {
        "total": 1,
        "page": 1,
        "pageSize": 5,
        "rows": [
            {
                "id": 1821556,
                "result": "Successful connection",
                "cycle": 1,
                "time": "2019-08-09 00:01:00",
		"start_time": "2019-09-09 09:00:01",
		"end_time": "2019-09-09 09:00:04",
                "phone": "85987053821",
                "second": 3,
                "voice_type": 2,
                "countryCode": "55",
                "messageid": 35618,
                "customer_price": 0.012,
                "show_phone": "1547822456",
                "size": 3
            }
        ]
    }
}
```

**Response Parameter Description:**
*1. Voice group call*

| Parameter      | Type   | Description       |
|:---------------|:-------|:------------------|
| code           | string | Interface return value: 0 for failure, 1 for success |
| phone          | string | Called number     |
| show_phone     | string | Displayed number  |
| countryCode    | string | Country code      |
| messageid      | string | messageid         |
| basic_price    | string | Basic fee for unsuccessful calls |
| second         | number | Duration in seconds |
| cycle          | number | Billing cycle     |
| size           | string | Number of cycles  |
| customer_price | string | Customer unit price |
| time           | string | Connection time   |
| start_time     | string | Call start time   |
| end_time       | string | Call end time     |
| result         | string | Sending result    |
| ivr_result     | string | Keypress feedback |

*2. Voice verification/notification*

| Parameter      | Type   | Description       |
|:---------------|:-------|:------------------|
| code           | string | Interface return value: 0 for failure, 1 for success |
| phone          | string | Called number     |
| show_phone     | string | Displayed number  |
| countryCode    | string | Country code      |
| messageid      | string | messageid         |
| second         | number | Duration in seconds |
| cycle          | number | Billing cycle     |
| size           | string | Number of cycles  |
| customer_price | string | Customer unit price |
| voice_type     | string | Voice service type: 1 for verification, 2 for notification |
| time           | string | Connection time   |
| start_time     | string | Call start time   |
| end_time       | string | Call end time     |
| result         | string | Sending result    |

