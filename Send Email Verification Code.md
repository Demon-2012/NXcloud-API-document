**Brief Description:**
- Sending email verification code

**Request Method:**
- URL: `http://api2.nxcloud.com/api/email/otp`
- Method: `POST`
- Content-Type: `application/json`

**Parameters:**
###### **Headers:**
|Parameter|Parameter Value|Required|Type|Description|
|:----    |:---|:----- |:-----   |:-----   |
|Content-Type |application/json  |  Yes |   |   |  |
###### **Body:**
|Parameter|Type|Required|Description|
|:----    |:----- |:-----   |:-----   |
|appKey |string  |Yes   |  Email application appKey |
|secretKey |string  |Yes   |  Email application secretKey |
|from |string  |Yes   |  Sender's email, must be in email address format |
|to |string  |Yes   |  Recipient's email, must be in email address format |
|templateName |string  |Yes   |  Template name |
|templateData |object  |No   |  Custom replacement data in the template, please make sure to insert replacement parameters in the template  |
|-- eAddr |string  |No   |  Address  |
|-- userName |string  |No   |  Customer's name  |
|-- nickName |string  |No   |  Customer's nickname  |
|-- gender |string  |No   |  Honorific, such as Mr., Ms.  |
|-- date |string  |No   |  Date, time  |
|-- mobile |string  |No   |  Mobile number  |
|-- vCode |string  |No   |  Verification code  |

**Request Example**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/email/otp' \
--header 'Content-Type: application/json' \
--data-raw '{
    "appKey": "asdf",
    "secretKey": "qwer",
    "from": "asdf@qwer.com",
    "to": "qwer@asdf.com",
    "templateName": "temp1",
    "templateData": {
        "eAddr": "",
        "userName": "",
        "nickName": "",
        "gender": "",
        "date": "",
        "mobile": "",
        "vCode": "123456"
    }
}'
```

**Response Example**
``` 
{
    "msg": "Request succeeded",
    "result": "e7b3082a46cf4959a3bc10f5d101d1cc",
    "code": 0
}
```

**Response Parameter Description**

|Parameter|Type|Description|
|:----    |:---  |:-----   |
|msg |string  |  Response message |
|result |string  |  Email ID |
|code |string  |  Response code |

**Error Codes**

|Code|Description|
|:----- |-----|
|0 |Request succeeded  | 
|601001 |Account status exception   |
|601002   |Insufficient account balance   |
|601101 |Application status exception, appKey/SecretKey mismatch   |
|601102 |No quotation for the application   |
|601103   |No domain configuration under the application|
|601104 |Domain not verified |
|601105 |Sender's email address does not exist   |
|601106   |Email template does not exist   |
|601107     |Email template not approved   |
|601201     |Submission failed   |