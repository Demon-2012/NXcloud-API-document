**Brief Description:** 
- Used forQueryReal-time QueueStatus

**RequestURL：** 
- ` http://api.nxcloud.com/api/queue/state `
  
**Request Method:**
- POST 

**Parameters：** 

|Parameter Name|Required|Type|Description|
|:----    |:---|:----- |-----   |
|appkey |Yes  |string |Approval FormApplicationappkey   |
|secretkey |Yes  |string | Approval FormApplicationsecretkey    |
|queueid     |Yes  |string | Queueid    |  

 **Return Example**

``` 
{
    "code": "0",
    "state": "1",
    "info": "success"
}
```

 **Return ParametersDescription** 

|Parameter Name|Type|Description|
|:-----  |:-----|-----                           |
|code |string   |0 IndicatesSuccess，OtherIndicatesFailure  |
|state |string   |StatusValue 0 NotCall 1 StartCall 2 Pause 3 Marked as Complete 4 Marked as Cancelled  |  

 **Remarks** 
- Without