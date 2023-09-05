
    
**Brief Description:** 

- Short LinkInterface List
  
**Request Method:**
- URL：`http://api.nxcloud.com/api/shortLink/shortLinks`
- Method：`POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters：** 

|Parameter Name|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey |Yes  |string | SMSApplicationappkey  |
|secretkey |Yes  |string | SMSApplicationsecretkey  |
|url |Yes  |string |Long Connection(PleaseUseOriginalLong Connection)|

**RequestExample：**
```shell
curl --location --request POST 'http://api.nxcloud.com/api/shortLink/shortLinks' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'url=www.asdfghjklzxcvbnm.com'
```

 **Return Example**

``` 
 {
    "code": "0",
    "row": [
		{"short_link":"http://xxx/xxxxxx"},
		{"short_link":"http://xxx/xxxxx2"}
	]
}
```

 **Return ParametersDescription** 

|Parameter Name|Type|Description|
|:-----  |:-----|-----|
|code |string   |ResultEncoding |
|row |array   | ManyShort LinkInterface |

 **Remarks**

Error Code

|code|Description|
|:----- |-----|
|0 |RequestSuccess  | 
|1 |ApplicationNotAvailableorkeyError   |
|2 |ParametersErrororisEmpty   |
|3 |BalanceNotSufficient   |
|9 |IPIllegal   |
|11 |Incorrect Email Format|
|88 |RequestFailure  |
|99 |SystemError   |
