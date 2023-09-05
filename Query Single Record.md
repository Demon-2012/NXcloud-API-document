**Brief Description:**
- Query Single Record  

**RequestURL：**
-  `http://api2.nxcloud.com/opt/call/get`

**Request Method:**
-  GET
  ```
  GET http://api2.nxcloud.com/otp/call/get?requestId=ce21811804a449a08e07e61ba7c52824&appkey=aaa&appsecret=bbb 
   ```
**RequestParameters：**  

  |Parameter Name|Type|Description|
  |:-----  |:-----|-----|
  |appkey |string   |NiuXin Platform，flash call of the Application app key |
  |secretkey |string   |NiuXin Platform，flash call of the Application secret key |
  |requestId |string   |InvocationInitiate flash call Interface，Returned requestId |  

**Return Example**
```
{
  "cdr": {
    "id": 44,
    "customerId": 1,
    "appId": 1,
    "msisdn": " 628618628952558",
    "callingNumber": "2150928922",
    "token": "8922",
    "requestId": "ce21811804a449a08e07e61ba7c52824",
    "ip": "127.0.0.1",
    "price": 0.0,
    "cost": 0.0,
    "gmtCreate": "2021-04-29T02:52:21.000+0000",
    "gmtModified": null,
    "callStartAt": null,
    "callEndAt": null,
    "callbackAt": null,
    "callStatus": 0
  },
  "code": "0"
}
```

**Return ParametersDescription**

  |Parameter Name|Type|Description|
  |:-----  |:-----|-----|
  |code |string   |ResultEncoding，is0YesSuccess，Others areYesFailure，Specifically refer toFailureCode table |
  |cdr |json   |IfcodeNotis0，RepresentsFailure；<br/>codeis0，ThenisThis timeQueryRecord； <br/> IfValueis null，Represents requestIdIncorrect； |  

