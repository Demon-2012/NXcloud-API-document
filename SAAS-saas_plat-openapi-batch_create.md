# Batch Create Customers
Batch create customers
- URL: `https://api.nxcloud.com/saas/cdp/openapi/customers/batch_create`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Request Parameters

### Header Parameters:

| Parameter Name | Type    | Required | Example Value                    | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| accessKey      | String  | Yes      | fme2na3kdi3ki                    | User identity identifier                                                                     |
| ts             | String  | Yes      | 1655710885431                    | Current request timestamp (in milliseconds). The maximum allowed time difference is 60 seconds |
| bizType        | String  | Yes      | 2                                | WhatsApp business type, fixed value "2"                                                      |
| action         | String  | Yes      | mt                               | WhatsApp business operation, fixed value "mt"                                                 |
| sign           | String  | Yes      | 6e9506557d1f289501d333ee2c365826 | API input parameter signature, common convention                                               |

### Body Parameters:

| Parameter Name | Type    | Required | Example Value                    | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| type           | integer | Yes      | 1                                | 0: Discard old data and use new data, 1: Update/add data based on old data, 2: Keep old data and discard new data |
| tenant_id      | integer | Yes      | 123                              | Tenant ID                                                                                     |
| app_key        | string  | Yes      | 46oKF=os                         | App key                                                                                       |
| customers      | array   | Yes      | customers information            | Batch creation, limited to 100 at a time                                                      |

#### Message Types

- customers parameters:

| Parameter Name   | Type    | Required | Example Value                    | Description                   |
| ---------------- | ------- | -------- | -------------------------------- | ----------------------------- |
| first_name       | String  | Yes      | -                                | First Name, maximum length of 128 characters |
| last_name        | String  | Yes      | -                                | Last Name, maximum length of 128 characters |
| sms_phone        | String  | No       | -                                | Phone number, maximum length of 30 characters |
| whats_app_phone  | String  | No       | -                                | WhatsApp, maximum length of 30 characters |
| country          | String  | No       | -                                | Country, maximum length of 50 characters |
| email            | String  | No       | -                                | Email, maximum length of 50 characters |
| address          | String  | No       | -                                | Street, maximum length of 100 characters |
| birthday         | String  | No       | -                                | Birthday, format: yyyy-MM-dd |
| tagStr           | String  | No       | -                                | Tags |
| remark           | String  | No       | -                                | Remark, maximum length of 100 characters |
| time_zone        | String  | No       | -                                | Time zone |
| gender           | integer | No       | -                                | Gender, 1: Male, 0: Female |
| customize_field  | String  | No       | -                                | Custom field data |

## Request Example

### Batch Create Request Example
Body (application/json) parameters:
```json
{
    "type": 0,
    "tenant_id": 144,
    "customers": [
        {
            "first_name": "张",
            "last_name": "三",
            "sms_phone": "18163725558",
            "whats_app_phone": "18667728886",
            "country": "中国",
            "email": "n.yxceiqtqc@qq.com",
            "address": "贵州省威海市东坡区",
            "birthday": "1976-04-12",
            "source": "voluptate Excepteur",
            "remark": "nisi amet",
            "tagStr": "test,99",
            "time_zone": "GMT+8",
            "gender": 0,
            "customize_field": "{\"customize_1_14\": \"aa\"}"
        },
        {
            "first_name": "李",
            "last_name": "四",
            "sms_phone": "18135539411",
            "whats_app_phone": "18178516529",
            "country": "中国",
            "email": "o.kleejvdy@qq.com",
            "address": "福建省泰安市武进区",
            "birthday": "2015-08-19",
            "source": "aliquip laboris dolore",
            "remark": "ut",
            "time_zone": "GMT+8",
            "tagStr": "88,99",
            "gender": 1
        }
    ]
}
```

## Response Parameters

| Parameter Name | Type    | Description     |
| -------------- | ------- | --------------- |
| code           | Integer | Result code     |
| data           | JsonObject | Request result  |
| message        | String  | Request message |
| traceId        | String  | Trace ID        |

## Response Example

### Successful Example
```json
{
	"code": 0,
	"message": "",
	"data": "",
	"traceId": "56bf81643292cd6a89ecde64ae00db13"
}
```