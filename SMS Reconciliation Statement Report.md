
    
**Brief Description：** 

- SMSStatementReport
  
**Request Method：**
- URL：`http://api2.nxcloud.com/api/sms/getSmsReport`
- Method：`POST`
- Content-Type：`application/x-www-form-urlencoded`

**Parameters：** 

|ParametersName|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey   |Yes|string |SMSApplicationappkey  |
|secretkey   |Yes|string |SMSApplicationsecretkey  |
|start_date   |Yes|string |StartTime（yyyy-MM-dd）  |
|end_date   |Yes|string |EndTime （yyyy-MM-dd） |

**Request Example：**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/sms/getSmsReport' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'start_date=2023-02-02' \
--data-urlencode 'end_date=2023-02-05'
```

**ReturnExample**

``` 
{
	"code": "0",
	"row": [
		{
			"total_fee": 14.25,
			"submit_size": 95,
			"success_size": 82,
			"price_size": 82
		}
	]
}
```

 **ReturnParametersDescription** 

|ParametersName|Type|Description|
|:-----  |:-----|-----|
|code |string   |InterfaceReturnValue|
|total_fee |number   |SMSCost |
|submit_size |number   | SMSSubmissions |
|success_size |number   |SuccessfulNumber |
|price_size |number   |ChargingNumber |

 **Remarks** 

- ErrorErrorCodeCode

|code|Description|
|:----- |-----|
|0 |success | 
|1|params invalid |
|2 |keys invalid | 
|5 |api request times invalid  | 