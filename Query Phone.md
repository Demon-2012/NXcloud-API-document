
    
**Brief Description:** 

- UserQuery PhoneInterface
  
**Request Method:**
- URL：`https://api.nxcloud.com/api/sipphone/queryMobs`
- Method：`POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters：** 

|Parameter Name|Required|Type|Description|
|:----    |:---|:----- |-----   |
|username |Yes  |string |UserLoginofUserName   |
|password |Yes  |string | UserLoginofSecretCode    |
|appkey     |No  |string | Approval Formofappkey    |
|page     |No  |int | Current Page(Default1)    |
|pageSize     |No  |int | Number of Items per Page(Default10)    |

**RequestExample：**
```shell
curl --location --request POST 'https://api.nxcloud.com/api/sipphone/queryMobs' \
--data-urlencode 'username=asdf' \
--data-urlencode 'password=qwer'
```

 **Return Example**

``` 
{
    "code": "success",
    "info": {
        "total": 1,
        "pageSize": 10,
        "page": 1,
        "rows": [
            {
                "monile_password": "1234qwer",
                "secretkey": "OvHlPwzz",
                "name": "aaa",
                "appkey": "NCZhOStw",
                "account": "wcj001",
                "username": "ali02990",
                "status": 0
            }
		]
	 }
}
```

 **Return ParametersDescription** 

|Parameter Name|Type|Description|
|:-----  |:-----|-----|
|code |string   | ReturncodeCode，successRepresentsSuccessReturnDataParametersWithoutError |
|total |int   | ReturnDataofTotal Count |
|pageSize |int   | Number of Displays per Day |
|page |int   | Current Page |
|rows |list   | PhoneResultSet |
|monile_password |string   | PhoneSecretCode |
|appkey |string   | PhoneCorrespondingApproval Formofappkey |
|secretkey |string   | PhoneCorrespondingApproval Formofsecretkey |
|account |string   | Approval FormAccount |
|name |string   | PhoneNickname |
|status |int   | PhoneStatus(0NotEnable，1Enable 2Disable) |
|username |string   | PhoneAccount |

 **ErrorParametersReturn** 

``` 
{
    "code": "failed",
    "info": "UserNameorSecretCodeError"
}
```
|Parameter Name|Type|Description|
|:-----  |:-----|-----|
|code |string   | ReturncodeCode，failedIndicatesParametersHaveError |
|info |string   | ErrorInformation |
