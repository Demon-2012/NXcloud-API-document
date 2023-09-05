**Brief Description：**

- SMSRecordThroughmessageidSingleQuery

**Request Method：**
- URL：`http://api2.nxcloud.com/api/sms/get`
- Method：`POST`
- Content-Type：`application/x-www-form-urlencoded`

**Parameters：** 

|ParametersName|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |SMSApplicationappkey  |
|secretkey   |Yes|string |SMSApplicationsecretkey  |
|date   |Yes|string |Date(yyyyMMdd)  |
|messageid   |Yes|string |PleaseRequestSMSSendInterfaceTimeReturnofmessageid |

**Request Example：**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/sms/ge' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'date=20230202' \
--data-urlencode 'messageid=qwer1234567890'
```

**ReturnExample**

``` 
{
    "code": "0",
    "row": {
        "billing_size": 1,
        "date": "2021-06-28 09:00:00",
        "senderid": "666",
        "phone": "6288888888888",
        "dr_time": "2021-06-28 09:00:00",
        "billing_price": 0.0,
        "msgid": "xxxxxxxxxxxxxxxxxxxxxxxx",
        "billing_status": "No",
        "body": "hello, your code is 888888",
        "dr_status": "Successful",
        "dr": "DELIVRD",
        "network": "PT TELEKOMUNIKASI SELULAR"
    }
}
```

 **ReturnParametersDescription** 

|ParametersName|Type|Description|
|:-----  |:-----|-----|
|code |string   |InterfaceReturnValue|
|senderid |string  |SMSsenderid |
|body |string   |SMSContent |
|phone |string   |Target NumberCode, WithCountry Code |
|msgid |string   |SMSid |
|dr_status |string   |SubmitStatus |
|billing_size |number   |BillingNumber |
|billing_price |number   |BillingUnit Price |
|date |string   |SendDate |
|dr_time |string   |drDate |
|billing_status |string   |BillingStatus |
|network |string   |Operator |
|dr |string   |OperatorReceipt |  

 **Remarks** 

- ErrorErrorCodeCode

|code|Description|
|:----- |-----|
|0 |success | 
|1|params invalid |
|2 |keys invalid | 
|3 |Only recent 31 days | 