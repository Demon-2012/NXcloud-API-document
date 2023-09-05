| **Error Code** | **Error Message** | **Error Reason/Solution**                                    |
| -------------- | ----------------- | ------------------------------------------------------------ |
| 1001           | Missing public parameters | All required [public parameters](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A#%E5%85%AC%E5%85%B1%E5%8F%82%E6%95%B0) must be included in the Header, such as accessKey, ts, bizType, action, sign |
| 1002           | Parameter error | Check if the `bizType` and `action` parameters in the Header are correct; Check if the parameters in the Body are correct |
| 1003           | Invalid signature | Check if the sign value calculation is correct. Common reasons for errors: 1. Incorrect request method, the correct Content-Type needs to be set (refer to the Content-Type in the API interface documentation); 2. The JSON string taken for signature calculation is different from the JSON string in the actual request body; 3. Signature calculation error, please refer to the [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A#yFiqL) for checking |
| 1004           | Timestamp expired | The ts parameter in the Header is incorrect. The maximum time difference allowed between the client and the server is 60 seconds |
| 1005           | Insufficient permissions | Incorrect accessKey or the current account does not have the corresponding business permissions |
| 10001          | Empty binding number | A or B number is empty |
| 10002          | Same binding number | A and B numbers are the same |
| 10003          | User does not exist | User does not exist |
| 10004          | Different prefix for binding numbers | A or B number does not contain the country code of the virtual number |
| 10005          | Failed to get number | Error occurred while getting the number of bound DIDs |
| 10006          | Exception in binding numbers | Exception occurred in the number of bound DIDs |
| 10007          | Virtual number without prefix | Virtual number does not have a country code |
| 10008          | User has no virtual number | User has no virtual number |
| 10009          | Failed to retrieve data | Exception occurred while retrieving data |
| 10010          | Virtual number exhausted | User's virtual numbers have been exhausted |
| 10011          | Incorrect list page capacity | The limit for retrieving data exceeds the range |
| 10012          | Incorrect list page starting point | The offset for retrieving data exceeds the range |
| 10013          | User has no binding number | User does not have a binding relationship with a virtual number |