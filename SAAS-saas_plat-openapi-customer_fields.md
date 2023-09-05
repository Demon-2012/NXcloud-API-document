# Query Customer Fields API
Query Customer Fields API
- URL: `https://api.nxcloud.com/saas/cdp/openapi/customers/fields`
- Method: `GET`
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

### Params Parameters:

| Parameter Name | Type    | Required | Example Value                    | Description                                                                                   |
| -------------- | ------- | -------- | -------------------------------- | ---------------------------------------------------------------------------------------------- |
| tenant_id      | integer | Yes      | 123                              | Tenant ID                                                                                     |
| app_key        | string  | Yes      | Lfap8mE                          | App key                                                                                       |
| is_preset      | boolean | No       | -                                | Optional. true: system preset, false: non-system preset. Display all if not provided          |

## Response Parameters

| Parameter Name | Type    | Description     |
| -------------- | ------- | --------------- |
| code           | Integer | Result code     |
| data           | array   | Request result  |
| message        | String  | Request message |
| traceId        | String  | Trace ID        |

- data array parameters:

| Parameter Name   | Type    | Description     |
| ---------------- | ------- | --------------- |
| id               | Integer | ID              |
| tenantId         | Integer | Tenant ID       |
| name             | String  | Field name      |
| display_name     | String  | Display name    |
| display_en_name  | String  | Display name (English) |
| is_display       | Boolean | Whether to display |
| field_type       | Integer | Field type      |
| required         | Boolean | Whether required |
| sequence         | String  | Field sequence  |
| remark           | String  | Remark          |
| field_type_info  | String  | Field type definition information |
| is_preset        | Boolean | Whether system preset |

## Response Example

### Successful Example
```json
{
    "code": 0,
    "message": "",
    "data": [
        {
            "id": 4071,
            "tenantId": 144,
            "name": "first_name",
            "required": false,
            "sequence": 1,
            "remark": null,
            "display_name": "First Name",
            "display_en_name": "First Name",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4072,
            "tenantId": 144,
            "name": "last_name",
            "required": false,
            "sequence": 2,
            "remark": null,
            "display_name": "Last Name",
            "display_en_name": "Last Name",
            "is_display": false,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4073,
            "tenantId": 144,
            "name": "sms_phone",
            "required": false,
            "sequence": 3,
            "remark": null,
            "display_name": "手机号码",
            "display_en_name": "Phone Number",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4074,
            "tenantId": 144,
            "name": "whats_app_phone",
            "required": false,
            "sequence": 4,
            "remark": null,
            "display_name": "WhatsApp",
            "display_en_name": "WhatsApp",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4075,
            "tenantId": 144,
            "name": "email",
            "required": false,
            "sequence": 5,
            "remark": null,
            "display_name": "邮箱",
            "display_en_name": "Email",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4076,
            "tenantId": 144,
            "name": "tags",
            "required": false,
            "sequence": 6,
            "remark": null,
            "display_name": "标签",
            "display_en_name": "Tag",
            "is_display": true,
            "field_type": 7,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4077,
            "tenantId": 144,
            "name": "created_at",
            "required": false,
            "sequence": 7,
            "remark": null,
            "display_name": "创建时间",
            "display_en_name": "Updated at",
            "is_display": true,
            "field_type": 6,
            "field_type_info": "{\"formatter\": \"yyyy-MM-dd HH:mm:ss\"}",
            "is_preset": true
        },
        {
            "id": 4078,
            "tenantId": 144,
            "name": "updated_at",
            "required": false,
            "sequence": 8,
            "remark": null,
            "display_name": "更新时间",
            "display_en_name": "Created at",
            "is_display": true,
            "field_type": 6,
            "field_type_info": "{\"formatter\": \"yyyy-MM-dd HH:mm:ss\"}",
            "is_preset": true
        },
        {
            "id": 4079,
            "tenantId": 144,
            "name": "country",
            "required": false,
            "sequence": 9,
            "remark": null,
            "display_name": "国家",
            "display_en_name": "Country",
            "is_display": false,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4080,
            "tenantId": 144,
            "name": "time_zone",
            "required": false,
            "sequence": 10,
            "remark": null,
            "display_name": "时区",
            "display_en_name": "Time Zone",
            "is_display": false,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4081,
            "tenantId": 144,
            "name": "age",
            "required": false,
            "sequence": 11,
            "remark": null,
            "display_name": "年龄",
            "display_en_name": "Age",
            "is_display": false,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": true
        },
        {
            "id": 4082,
            "tenantId": 144,
            "name": "birthday",
            "required": false,
            "sequence": 12,
            "remark": null,
            "display_name": "出生日期",
            "display_en_name": "The date of birth",
            "is_display": false,
            "field_type": 5,
            "field_type_info": "{\"formatter\": \"yyyy-MM-dd\"}",
            "is_preset": true
        },
        {
            "id": 4083,
            "tenantId": 144,
            "name": "gender",
            "required": false,
            "sequence": 13,
            "remark": null,
            "display_name": "性别",
            "display_en_name": "Gender",
            "is_display": false,
            "field_type": 3,
            "field_type_info": "[{\"id\": \"1\", \"name\": \"男\", \"i18nCode\": \"saas.plat.api.11156\"}, {\"id\": \"0\", \"name\": \"女\", \"i18nCode\": \"saas.plat.api.11188\"}]",
            "is_preset": true
        },
        {
            "id": 4136,
            "tenantId": 144,
            "name": "customize_1_13",
            "required": false,
            "sequence": 14,
            "remark": null,
            "display_name": "文本",
            "display_en_name": "文本",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": false
        },
        {
            "id": 4137,
            "tenantId": 144,
            "name": "customize_1_14",
            "required": false,
            "sequence": 15,
            "remark": null,
            "display_name": "自定义字段2",
            "display_en_name": "自定义字段2",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": false
        },
        {
            "id": 4138,
            "tenantId": 144,
            "name": "customize_1_15",
            "required": false,
            "sequence": 16,
            "remark": null,
            "display_name": "自定义字段 3",
            "display_en_name": "自定义字段 3",
            "is_display": true,
            "field_type": 1,
            "field_type_info": null,
            "is_preset": false
        },
        {
            "id": 4139,
            "tenantId": 144,
            "name": "customize_2_16",
            "required": false,
            "sequence": 17,
            "remark": null,
            "display_name": "数字",
            "display_en_name": "数字",
            "is_display": true,
            "field_type": 2,
            "field_type_info": null,
            "is_preset": false
        },
        {
            "id": 4140,
            "tenantId": 144,
            "name": "customize_3_17",
            "required": false,
            "sequence": 18,
            "remark": null,
            "display_name": "单选",
            "display_en_name": "单选",
            "is_display": true,
            "field_type": 3,
            "field_type_info": "[{\"id\": \"1\", \"name\": \"A\"}, {\"id\": \"2\", \"name\": \"B\"}, {\"id\": \"1682407283267\", \"name\": \"C\"}]",
            "is_preset": false
        },
        {
            "id": 4141,
            "tenantId": 144,
            "name": "customize_4_18",
            "required": false,
            "sequence": 19,
            "remark": null,
            "display_name": "多选",
            "display_en_name": "多选",
            "is_display": true,
            "field_type": 4,
            "field_type_info": "[{\"id\": \"1\", \"name\": \"A\"}, {\"id\": \"2\", \"name\": \"B\"}, {\"id\": \"1682407301578\", \"name\": \"C\"}]",
            "is_preset": false
        },
        {
            "id": 4142,
            "tenantId": 144,
            "name": "customize_5_19",
            "required": false,
            "sequence": 20,
            "remark": null,
            "display_name": "日期",
            "display_en_name": "日期",
            "is_display": true,
            "field_type": 5,
            "field_type_info": "{\"formatter\": \"yyyy-MM-dd\"}",
            "is_preset": false
        },
        {
            "id": 4143,
            "tenantId": 144,
            "name": "customize_6_20",
            "required": false,
            "sequence": 21,
            "remark": null,
            "display_name": "时间",
            "display_en_name": "时间",
            "is_display": true,
            "field_type": 6,
            "field_type_info": "{\"formatter\": \"yyyy-MM-dd HH:mm:ss\"}",
            "is_preset": false
        }
    ],
    "traceId": "148b351a19514993951c549dc7ddd077"
}
```