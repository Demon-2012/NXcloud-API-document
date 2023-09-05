
    
**Brief Description：** 

- SMSReceipt(DR)Push

**PleaseRequestURL：** 
- DRPushofHttpInterfaceAddress（ByUserProvided）
- `For Example： http://106.15.34.94:8989/sms/testDr `
  
**Request Method：**
- POST x-www-form-urlencoded
- 2023/5/4BeforeRegisterofCustomer，ParametersAturl；AfterofCustomer，ParametersAt post body 。

**Parameters：** 

|ParametersName|Required|Type|Description|
|:----    |:---|:----- |-----   |
|phone   |Yes|string |Phone Number  |
|status   |Yes|string |StatusCodeCode：2:SuccessfulBelowSend，OtherNumberWordAllNotBelowSendSuccessful |
|result   |Yes|string |ReceiptContent： DELIVRD\ UNDELIV |
|drtime   |Yes|string |ReceiptReportTime，FormatIs：yyyy-MM-dd HH:mm:ss |
|messageid   |Yes|string |SMSid，CorrespondingofSMSSubmitSuccessfulObtainedofid  |
|currency|Yes|string|priceofCurrency If：CNY\ USD|
|price   |Yes|string |CorrespondingCurrencyofSMSUnit Price  |
|rate   |Yes|string |USDToRMBExchange Rate If：7.05  |
|sendtime   |Yes|string |SendTime，FormatIs：yyyy-MM-dd HH:mm:ss |
|size|Yes|string|BillingNumber|
|ext   |No|string |Transparent TransmissionField，ThisFieldIsSMSBelowRowSendInterfaceInofNot NecessaryFillField，FillWriteAfterAtReceiptInWillOriginalReturn，Only Supportshttp |

 **PushExample**

2023/5/24 BeforeRegisterofCustomer，url PassParameters
``` 
POST http://106.15.34.94:8080/sms/testDr?result=DELIVRD&size=1&phone=6282167624806&rate=6.4845&price=0.045&messageid=b308d94a73f94e6d84ae975c41f4b2a6&drtime=2021-02-26 10:01:15&currency=USD&sendtime=2021-02-26 10:01:15&status=2
```

2023/5/24 AfterRegisterofCustomer，post body
``` 
POST http://106.15.34.94:8080/sms/testDr
Content-Type: x-www-form-urlencoded

result=DELIVRD&size=1&phone=6282167624806&rate=6.4845&price=0.045&messageid=b308d94a73f94e6d84ae975c41f4b2a6&drtime=2021-02-26 10:01:15&currency=USD&sendtime=2021-02-26 10:01:15&status=2
```

**ReceiptStatusCorrespondingCode**

```
public static final int DELIVRD = 2; // Successful
public static final int UNDELIV = 5; // Failure
public static final int REJECTD = 6; // Reject
public static final int EXPIRED = 7; // Expired
public static final int DELETED = 8; // Delete
public static final int DND = 9; // Do Not Disturb
public static final int ESME_RINVDSTADR = 10; // ErrorErrorNumberCode
public static final int ESME_RINVSRCADR = 11; // ErrorErrorSender
public static final int UNKNOWN = 12; // NotKnow
```

 **UserReturnValue**  
SuccessfulReturnWordString：success
FailureReturnWordString：error

 

 **Remarks**  
 Description：DROnlyPushOnce，IfFruitNeedRepeatPush，PleaseToCustomer ServiceContact
 BatchSMSofmessageid=responseofmessageid-10BitRandom Number（20190909151515701-1234567890）