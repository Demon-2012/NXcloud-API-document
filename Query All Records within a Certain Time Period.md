**Brief Description:**  
- Query All Records Within a Time Range

**RequestURL：**
-  `http://api2.nxcloud.com/opt/call/list`

**Request Method:**
- GET  
  ```
  GET http://api2.nxcloud.com/otp/call/list?start=2021-04-27%2017%3A00%3A00&end=2021-04-27%2018%3A00%3A00&appkey=aaa&appsecret=bbb 
  ```

**RequestParameters：**  

|Parameter Name|Type|Description|
|:-----  |:-----|-----|
|appkey |string   |NiuXin Platform，flash call of the Application app key |
|secretkey |string   |NiuXin Platform，flash call of the Application secret key |
|start |string   |QueryTime RangeofStartTime，Formatis： yyyy-MM-dd HH:mm:ss |
|end |string   |QueryTime RangeofEndTime，Formatis： yyyy-MM-dd HH:mm:ss |  

**Return Example**  
```
{
  "cdrs": [
    {
      "id": 4,
      "customerId": 1,
      "appId": 1,
      "msisdn": "182182182",
      "callingNumber": "2150928925",
      "token": "8925",
      "requestId": "3097f48a0c6e465586e9f7cc5a922b90",
      "ip": null,
      "price": 0.0,
      "gmtCreate": "2021-04-27 17:02:22",
      "gmtModified": null,
      "callStartAt": null,
      "callEndAt": null,
      "callbackAt": null,
      "callStatus": 0
    },
    {
      "id": 5,
      "customerId": 1,
      "appId": 1,
      "msisdn": "182182182",
      "callingNumber": "2150928927",
      "token": "8927",
      "requestId": "7674dc8e75774c09a470c3b0b0aa6a5d",
      "ip": null,
      "price": 0.0,
      "gmtCreate": "2021-04-27 17:02:44",
      "gmtModified": null,
      "callStartAt": null,
      "callEndAt": null,
      "callbackAt": null,
      "callStatus": 0
    }
  ],
  "code": "0"
}
```

**Return ParametersDescription**

  |Parameter Name|Type|Description|
  |:-----  |:-----|-----|
  |code |string   |ResultEncoding，is0YesSuccess，Others areYesFailure，Specifically refer toFailureCode table |
  |cdrs |json   | Meet the Conditionsof flash call CallRecord。<br/> ThisInterfaceNoHavePagination，Also Limits the MaximumReturnNumber 100。<br/> IfWantQueryMore，PleaseAbove the Last TimeReturnedThe Last Oneof gmtCreate Field，Asis start ParametersofValueReQuery|

