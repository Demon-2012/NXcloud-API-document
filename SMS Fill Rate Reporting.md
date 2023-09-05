**Brief Description：** 

- SMSFill RateReportInterface

**PleaseRequestURL：** 
- ` http://api2.nxcloud.com/api/smsdr/conversion `
  
**Request Method：**
- GET 
- Request Example：
![postman examples](https://github.com/nxtele/http-api-document/blob/main/shortLink.jpg)

**Parameters：** 

|ParametersName|Required|Type|Description|
|:----    |:---|:----- |-----   |
|messageid |Yes  |string |SMSSubmitTimeReturnofMessageID   |
|phone |No  |string | Phone NumberCode    |
|status     |No  |string | 10 IndicateReturnFillSuccessful(FillOtherValueOrEmptyWordString，AllWill Be ProcessedIsNotReturnFill)    |

 **UserReturnValue**  
SuccessfulReturnWordString：success  
FailureReturnWordString：fail

 **Remarks** 

- IfPleaseRequestNotWithstatus，ThenDefaultIsSuccessfulReturnFill