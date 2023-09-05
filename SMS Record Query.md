    
**Brief Description：** 

- SMSRecordQuery。Only SupportQueryRecently31DaysofSMSRecord，PleaseTimelyQuery。IfNeedFull AmountSMSRecordMaintenance，Can Also UseReceiptCallbackFunction，AutomaticReceiveDataAndSave。

**Request Method：**
- URL：`http://api2.nxcloud.com/api/sms/getSmsCdr`
- Method：`POST`
- Content-Type：`application/x-www-form-urlencoded`

**Parameters：** 

|ParametersName|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |SMSApplicationappkey  |
|secretkey   |Yes|string |SMSApplicationsecretkey  |
|date   |Yes|string |Date(yyyyMMdd)  |
|page_size   |Yes|string |Quantity （Less Than1000Items） |
|page   |Yes|string |StartPage  |
|sort_type   |No|string |SortType: 0=Ascending，1=Descending；DefaultIs0  |

**Request Example：**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/sms/getSmsCdr' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'date=20230202' \
--data-urlencode 'page_size=10' \
--data-urlencode 'page=1'
```

 **ReturnExample**

``` 
{
	"code": "0",
	"info": {
			"total": 1119,
			"page": 112,
			"pageSize": 2,
			"rows": [
				{
					"senderid": "",
					"body": "hello sms test 001.",
					"phone": "62833935195",
					"msgid": "5cd1397f-f3b2-95de-ed5e-27d5f39a230d",
					"dr_status": "Successful",
					"billing_size": 2,
					"billing_price": 0.09,
					"date": "2019-06-15 23:40:00",
					"dr_time": "2019-06-15 23:42:00",
					"billing_status": "Yes",
					"network": 893,
					"dr":"DELIVRD"
				},
				{
					"senderid": "",
					"body": "hello sms test 002.",
					"phone": "62844049494",
					"msgid": "f76bc33281124f8aa8bca33ce54b01ad",
					"dr_status": "Successful",
					"billing_size": 2,
					"billing_price": 0.09,
					"date": "2019-06-15 23:50:04",
					"dr_time": "2019-06-15 23:53:00",
					"billing_status": "Yes",
					"network": 791,
					"dr":"DELIVRD"
				}
				]
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
|3 |page_size or page_index  invalid | 
|4 |page_size or page_index invalid | 
|5 |api request times invalid  | 