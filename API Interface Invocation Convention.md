## Request Method ##

- Please refer to the documentation of each API interface and specify the correct Content-Type in the request header parameters.
- Please refer to the documentation of each API interface and specify the correct Content-Type in the request header parameters.
- Please refer to the documentation of each API interface and specify the correct Content-Type in the request header parameters.

<br/>

<a name="ggcs"></a>
## Common Parameters ##

The common parameters that must be included in the request header when calling the API interface are as follows:

| **Parameter Name** | **Parameter Type** | **Required** | **Example Value**                | **Parameter Description**                                    |
| ------------------ | ------------------ | ------------ | -------------------------------- | ------------------------------------------------------------ |
| accessKey          | String             | Yes          | fme2na3kdi3ki                    | User identity identifier                                     |
| ts                 | String             | Yes          | 1655710885431                    | Timestamp of the current request (in milliseconds). The maximum time difference allowed between the user and the server is 60000 milliseconds. |
| bizType            | String             | Yes          | 1                                | [Business type](#hGhKK)                                       |
| action             | String             | Yes          | send                             | API interface method. The parameter value should follow the instructions in the API interface documentation. |
| sign               | String             | Yes          | 6e9506557d1f289501d333ee2c365826 | Signature of the input parameters. [Signature algorithm](#yFiqL) |

<br/>
<a name="hGhKK"></a>

**Explanation of bizType parameter:**

| **Parameter Value** | **Business Description** |
| ------------------- | ------------------------ |
| 1                   | Number check             |
| 2                   | WhatsApp business        |
| 3                   | SMS                      |
| 4                   | DID business             |
| 5                   | Virtual number           |
| 6                   | OTA                      |
| 7                   | Viber                    |

<a name="yFiqL"></a>

<br/>

## Signature Algorithm ##

To prevent malicious tampering during API calls, the API interface needs to be accompanied by a request signature. The Open Platform server will verify the signature based on the request parameters, and requests with invalid signatures will be rejected.

**Signature Algorithm**:
- For API interfaces with a request method of `application/json`, the signature algorithm is: **`hex(md5(headersStr + bodyStr + accessSecretStr))`**
- For API interfaces with a request method of `multipart/form-data`, the signature algorithm is: **`hex(md5(headersStr + accessSecretStr))`**

**Signature Explanation**:
<br />
1. **headersStr**: Concatenate all required header parameters (except `sign`) in the header, sort the fields in ascending ASCII order, and concatenate them in the format of `key=val` with `&` in between. The resulting concatenated string is `accessKey=YOUR_ACCESS_KEY&action=ACTION&bizType=BIZ_TYPE&ts=CURRENT_TIMESTAMP`.
2. **bodyStr**: Append `&body=body JSON string` to the string obtained in the previous step. Notes:
   1. For API interfaces with a request method of `multipart/form-data`, there is no need to append `bodyStr`. Skip this step.
   2. If the JSON string in the body is null or an empty string, there is no need to append `bodyStr`. Skip this step.
   3. The JSON string in the body used for calculating the signature must be the same as the actual JSON string in the request body.
   4. The JSON string in the body used for calculating the signature must be the same as the actual JSON string in the request body.
   5. The JSON string in the body used for calculating the signature must be the same as the actual JSON string in the request body.
3. **accessSecretStr**: The password corresponding to the accessKey, ending with `&accessSecret=YOUR_ACCESS_SECRET`.
4. Use the **MD5 algorithm** to generate the signature. Convert the resulting byte stream to **lowercase hexadecimal**.

<br/>

### Example Code for Calculating the Signature ###

#### Java ####
```java
/**
 * Generate API parameter signature demo
 */
@Test
public void generateSignDemo() {
    // Header parameters
    Map<String, String> headers = new HashMap<>(8);
    headers.put("accessKey", "fme2na3kdi3ki");
    headers.put("ts", "1655710885431");
    headers.put("bizType", "1");
    headers.put("action", "send");

    // Business parameters
    JSONObject postData = new JSONObject();
    postData.put("id", 10001);
    postData.put("name", "牛小信");
    String body = postData.toString();
    
    // AccessSecret corresponding to the accessKey
    String accessSecret = "abciiiko2k3";

    String sign = calcSign(headers, body, accessSecret);
    log.info("sign: {}", sign); // sign: 87c3560d3331ae23f1021e2025722354
}

/**
 * Calculate the sign signature
 *
 * @param headers      Public parameters in the request header
 * @param body         JSON string in the body
 * @param accessSecret Secret key
 * @return
 */
private String calcSign(Map<String, String> headers, String body, String accessSecret) {
    StringBuilder raw = new StringBuilder();

    // Step 1: Concatenate header parameters
    raw.append("accessKey=").append(headers.get("accessKey")).append("&action=").append(headers.get("action"))
            .append("&bizType=").append(headers.get("bizType")).append("&ts=").append(headers.get("ts"));
    log.info("step1: {}", raw); // step1: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431

    // Step 2: Concatenate body parameters
    if (StringUtils.isNotEmpty(body)) {
        raw.append("&body=").append(body);
    }
    log.info("step2: {}", raw); // step2: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"name":"牛小信","id":10001}

    // Step 3: Concatenate accessSecret
    raw.append("&accessSecret=").append(accessSecret);
    log.info("step3: {}", raw); // step3: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"name":"牛小信","id":10001}&accessSecret=abciiiko2k3

    // Step 4: Encrypt with MD5 algorithm and convert the result to lowercase hexadecimal
    String sign = DigestUtils.md5Hex(raw.toString());
    log.info("step4: sign={}", sign); // step4: sign=87c3560d3331ae23f1021e2025722354

    return sign;
}
```

<br/>

#### C# ####

```csharp
public static void Main() {

    // Header parameters
    Dictionary<string, string> headers = new Dictionary<string, string>();
    headers.Add("accessKey", "fme2na3kdi3ki");
    headers.Add("ts", "1655710885431");
    headers.Add("bizType", "1");
    headers.Add("action", "send");

    // Business parameters
    string body = "{\"name\":\"牛小信\",\"id\":10001}";

    // AccessSecret corresponding to the accessKey
    string accessSecret = "abciiiko2k3";
    
    string sign = calcSign(headers, body, accessSecret);
    Console.WriteLine("sign: {0}", sign); // sign: 87c3560d3331ae23f1021e2025722354
}


/**
 * Calculate the sign signature
 *
 * @param headers      Public parameters in the request header
 * @param body         JSON string in the body
 * @param accessSecret Secret key
 * @return
 */
public static string calcSign(IDictionary<string, string> headers, String body, string accessSecret) {
    StringBuilder str = new StringBuilder();
    
    // Step 1: Concatenate header parameters
    str.Append("accessKey=").Append(headers["accessKey"]).Append("&action=").Append(headers["action"])
        .Append("&bizType=").Append(headers["bizType"]).Append("&ts=").Append(headers["ts"]);
    Console.WriteLine("step1: {0}", str); // step1: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431
    
    // Step 2: Concatenate body parameters
    if (!string.IsNullOrEmpty(body)) {
        str.Append("&body=").Append(body);
    }
    Console.WriteLine("step2: {0}", str); // step2: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"name":"牛小信","id":10001}
    
    // Step 3: Concatenate accessSecret
    str.Append("&accessSecret=").Append(accessSecret);
    Console.WriteLine("step3: {0}", str); // step3: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"name":"牛小信","id":10001}&accessSecret=abciiiko2k3
    
    // Step 4: Encrypt with MD5 algorithm and convert the result to lowercase hexadecimal
    MD5 md5 = MD5.Create();
    byte[] bytes = md5.ComputeHash(Encoding.UTF8.GetBytes(str.ToString()));
    StringBuilder result = new StringBuilder();
    for (int i = 0; i < bytes.Length; i++)
    {
        result.Append(bytes[i].ToString("x2"));
    }
    string sign = result.ToString();
    Console.WriteLine("step4: sign={0}", sign); // step4: sign=87c3560d3331ae23f1021e2025722354


    return sign;
}
```

<br/>

#### PHP ####

```php
<?php

$headers = array("accessKey" => "fme2na3kdi3ki", "ts" => "1655710885431", "bizType" => "1", "action" => "send");
$postData = array("id" => 10001, "name" => "牛小信");
$body = json_encode($postData, JSON_UNESCAPED_UNICODE);
echo "body= " . $body . "\n"; // body= {"id": 10001, "name": "牛小信"}

$accessSecret = "abciiiko2k3";
$sign = calcSign($headers, $body, $accessSecret);
echo "sign=" . $sign; // sign=7750759da06333f20d0640be09355e34


/**
  * Calculate the sign signature
  *
  * @param headers      Public parameters in the request header
  * @param body         JSON string in the body
  * @param accessSecret Secret key
  * @return
  */
function calcSign($headers, $body, $accessSecret) {
    // Step 1: Concatenate header parameters
    $str = "accessKey=".$headers['accessKey']."&action=".$headers['action']
        ."&bizType=".$headers['bizType']."&ts=".$headers['ts'];
    echo "step1: " . $str . "\n"; // step1: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431
    
    // Step 2: Concatenate body parameters
    if (!empty($body)) {
        $str = $str . "&body=" . $body;
    }
    echo "step2: " . $str . "\n"; // step2: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id":10001,"name":"牛小信"}
    
    // Step 3: Concatenate accessSecret
    $str = $str . "&accessSecret=" . $accessSecret;
    echo "step3: " . $str . "\n"; // step3: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id":10001,"name":"牛小信"}&accessSecret=abciiiko2k3
    
    // Step 4: Encrypt with MD5 algorithm and convert the result to lowercase hexadecimal
    $ret = md5($str);
    echo "step4: sign=" . $ret . "\n"; // step4: sign=7750759da06333f20d0640be09355e34

    return $ret;
}

?>
```

<br/>

#### Python ####

```python
'''
Calculate the sign signature
headers      Public parameters in the request header
body         JSON string in the body
accessSecret Secret key
'''
def calc_sign(headers, body, accessSecret):
    # Step 1: Concatenate header parameters
    string_raw = 'accessKey=' + str(headers['accessKey']) + '&action=' + str(headers['action']) + '&bizType=' + str(headers['bizType'])  + '&ts=' + str(headers['ts']) 
    print("step1:",string_raw); # step1: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431
    
    # Step 2: Concatenate body parameters
    if len(body) > 0:
        string_raw += '&body=' + body
    print("step2:",string_raw); # step2: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id": 10001, "name": "牛小信"}
    
    # Step 3: Concatenate accessSecret
    string_raw += '&accessSecret=' + accessSecret
    print("step3:",string_raw); # step3: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id": 10001, "name": "牛小信"}&accessSecret=abciiiko2k3

    # Step 4: Encrypt with MD5 algorithm and convert the result to lowercase hexadecimal
    sign = hashlib.md5(string_raw.encode()).hexdigest()
    print("step4: sign=",sign); # step4: sign= d0c24a9886c629330d7f3f2056c65bc2
    return sign


headers = {'accessKey':'fme2na3kdi3ki','ts':'1655710885431','bizType':'1','action':'send'}

params = {'id':10001,'name':'牛小信'}
body = json.dumps(params, ensure_ascii=False)
print("body=", body) # body= {"id": 10001, "name": "牛小信"}

accessSecret = 'abciiiko2k3'

sign = calc_sign(headers, body, accessSecret)
print("sign=", sign) # sign= d0c24a9886c629330d7f3f2056c65bc2
```

<br/>

#### Go ####

```go
func main() {
    
    headers := map[string]string{
        "accessKey": "fme2na3kdi3ki",
    	"ts": "1655710885431",
   		"bizType": "1",
    	"action": "send",
	}
	
	postData := map[string]interface{}{
        "id": 10001,
    	"name": "牛小信",
	}
    bodyByte, err := json.Marshal(postData)
    if err != nil {
      fmt.Printf("序列号错误 err=%v\n", err)
    }
    body := string(bodyByte)
	fmt.Println("body:", body) // body: {"id":10001,"name":"牛小信"}

    accessSecret := "abciiiko2k3"

    sign := calcSign(headers, body, accessSecret)
    fmt.Println("sign:", sign) // sign: 7750759da06333f20d0640be09355e34
}


/**
 * Calculate the sign signature
 *
 * @param headers      Public parameters in the request header
 * @param body         JSON string in the body
 * @param accessSecret Secret key
 * @return
 */
func calcSign(headers map[string]string, body string, accessSecret string) string {
    var build strings.Builder
    
    // Step 1: Concatenate header parameters
    build.WriteString("accessKey=");
    build.WriteString(headers["accessKey"]);
    build.WriteString("&action=");
    build.WriteString(headers["action"]);
    build.WriteString("&bizType=");
    build.WriteString(headers["bizType"]);
    build.WriteString("&ts=");
    build.WriteString(headers["ts"]);
    fmt.Println("step1:", build.String()) // step1: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431
    
    // Step 2: Concatenate body parameters
    if len(body) > 0 {
        build.WriteString("&body=");
        build.WriteString(body);
    }
    fmt.Println("step2:", build.String()) // step2: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id":10001,"name":"牛小信"}
    
    // Step 3: Concatenate accessSecret
    build.WriteString("&accessSecret=")
    build.WriteString(accessSecret)
    raw := build.String();
    fmt.Println("step3:", raw) // step3: accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"id":10001,"name":"牛小信"}&accessSecret=abciiiko2k3    
    // Step 4: Encrypt with MD5 algorithm and convert the result to lowercase hexadecimal
    md5Result := md5.Sum([]byte(raw))
    sign := fmt.Sprintf("%x", md5Result)
    fmt.Println("step4: sign=", sign) // step4: sign= 7750759da06333f20d0640be09355e34

    return sign
}
```

<br/>

## Example of API Invocation ##
Taking the API interface with a request method of `application/json` as an example, the signature invocation process is as follows:
> **1. Set parameter values**
- Public parameters in the header:
   - `accessKey: fme2na3kdi3ki`
   - `bizType: 1`
   - `action: send`
   - `ts: 1655710885431`
- Body parameter:
   - `{"name":"牛小信","id":10001}`

<br/>

> **2. Concatenate Header, body, and accessSecret**

`accessKey=fme2na3kdi3ki&action=send&bizType=1&ts=1655710885431&body={"name":"牛小信","id":10001}&accessSecret=abciiiko2k3`

<br/>

> **3. Generate the Signature**

According to the signature algorithm: `hex(md5(headersStr + bodyStr + accessSecretStr))` <br />Perform MD5 encryption and convert the result to lowercase hexadecimal. sign:`87c3560d3331ae23f1021e2025722354`

<br/>

> **4. Assemble the HTTP Request**

Add the signature to the Header and send the HTTP request. The final request Header and body are as follows:

- Public parameters in the header:
   - `accessKey: fme2na3kdi3ki`
   - `bizType: 1`
   - `action: send`
   - `ts: 1655710885431`
   - `sign: 87c3560d3331ae23f1021e2025722354`
- Body parameter:

   - `{"name":"牛小信","id":10001}`

<br/>

<a name="cjcwm"></a>
## Common Error Codes ##

| **Error Code** | **Error Message** | **Error Cause/Solution**                                      |
| -------------- | ----------------- | ------------------------------------------------------------ |
| 1001           | Missing parameters | All required [common parameters](#ggcs) must be included in the Header. |
| 1002           | Parameter error   | Check if the `bizType` and `action` parameters in the Header are correct;<br/>Check if the parameters in the Body are correct. |
| 1003           | Invalid signature | Check if the sign value is calculated correctly. Common causes of errors include:<br>1. Incorrect request method. Set the correct Content-Type in the request header parameters (refer to the Content-Type in the API interface documentation).<br>2. The JSON string in the body used for calculating the signature is different from the actual JSON string in the request body (e.g., if the actual request body JSON string contains line breaks, the body string used for calculating the signature must also contain line breaks).<br>3. Incorrect accessSecret.<br>4. Signature calculation error. Refer to the [signature algorithm](#yFiqL) for verification. |
| 1004           | Timestamp expired | The ts parameter in the Header is incorrect. The timestamp passed should be in milliseconds, and the maximum time difference allowed between the user and the server is 60000 milliseconds. |
| 1005           | Insufficient permissions | The accessKey is incorrect or the current account does not have the corresponding business permissions. |