
    
**Brief Description:** 

- QueryThisUserAccountBelowofSoHaveofApproval Form

  
**Request Method:**
- URL：`https://api.nxcloud.com/api/sipphone/queryApps`
- Method：`POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters：** 

|Parameter Name|Required|Type|Description|
|:----    |:---|:----- |-----   |
|username |Yes  |string | UserLoginCloud PlatformofAccount   |
|password |Yes  |string | UserLoginCloud PlatformofSecretCode   |

**RequestExample：**
```shell
curl --location --request POST 'https://api.nxcloud.com/api/sipphone/queryApps' \
--data-urlencode 'username=asdf' \
--data-urlencode 'password=qwer'
```

 **Return Example**

``` 
{
    "code": "success",
    "row": [
        {
            "secretkey": "ZeaTkTAr",
            "name": "test321",
            "appkey": "ifHU1a33",
            "account": "test321"
        },
        {
            "secretkey": "OvHlPwzz",
            "name": "wcj_001",
            "appkey": "NCZhOStw",
            "account": "wcj001"
        }
	 ]
}
```

 **Return ParametersDescription** 

|Parameter Name|Type|Description|
|:-----  |:-----|-----  |
|code |string | success,RepresentsReturnRequestSuccess  |
|row |list | UserBelowSoHaveofApproval FormData  |
|appkey |string | Approval Formappkey  |
|secretkey |string | Approval Formsecretkey  |
|name |string | ThisApproval FormofNameWord  |
|account |string | ThisApproval FormofAccount  |

 **ReturnErrorInformation** 

``` 
{
    "code": "failed",
    "info": "UserNameorSecretCodeError"
}
```
|Parameter Name|Type|Description|
|:-----  |:-----|-----  |
|code |string | failed,RepresentsReturnDataFailure  |
|info |string | ErrorInformation  |
