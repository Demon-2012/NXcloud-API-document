# Query Phone Number List of Customer Applications (For Integrators Only)

Query the phone number list of customer applications through the API.

- URL: `https://api2.nxcloud.com/api/wa/integrator/embedded/register/phoneList`
- Method: `POST`
- Content-Type: `application/json`
- Requires authentication: Yes

## Authentication Mechanism

Please refer to the following link for authentication rules: [API Interface Call Convention](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A)

## Request Parameters
### Header Parameters:

| Parameter Name | Type   | Required | Example  | Description                                                 |
| -------------- | ------ | -------- | -------- | ----------------------------------------------------------- |
| accessKey      | String | Yes      | fmexxx3ki | User identity identifier                                    |
| ts             | String | Yes      | 1655710885431 | Current timestamp of the request (in milliseconds). The maximum allowed time difference is 60 seconds on the server side. |
| bizType        | String | Yes      | 2        | WhatsApp business type, fixed value "2"                      |
| action         | String | Yes      | phoneList | WhatsApp business operation, fixed value "phoneList"         |
| sign           | String | Yes      | 6e95xxx826 | API input parameter signature, [signature algorithm](https://github.com/nxtele/http-api-document/wiki/API%E6%8E%A5%E5%8F%A3%E8%B0%83%E7%94%A8%E7%BA%A6%E5%AE%9A) |

### Body Parameters:

| Parameter Name | Type   | Required | Example | Description                                                  |
| -------------- | ------ | -------- | ------- | ------------------------------------------------------------ |
| appkey         | String | Yes      |         | Appkey of the NxCloud WhatsApp application                   |

## Request Example
Body (application/json) parameters:
```json
{
    "appkey": "jh42xxxd434"
}
```

## Response Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| code           | Integer    | Result code   |
| data           | JsonObject | Request result |
| message        | String     | Request result description |

- data object parameters:

| Parameter Name | Type   | Description                 |
| -------------- | ------ | --------------------------- |
| display_phone_number | string | Registered WhatsApp number |
| quality_rating       | string | Number quality rating. Enum values: GREEN: High quality; YELLOW: Medium quality; RED: Low quality; UNKNOW: Quality unknown |
| verified_name        | string | Display name of the number |
| name_status          | string | Name verification status. Enum values: APPROVED: Name has not been approved; NONE: No available certificate; AVAILABLE_WITHOUT_REVIEW: Certificate for downloading phone number is available without review; DECLINED: Name has not been approved. You cannot download the certificate; EXPIRED: Your certificate has expired and cannot be downloaded; PENDING_REVIEW: Your name request is under review. You cannot download the certificate |
| register_status      | integer| Connection status. <br>1: Creation failed (local client)<br>2: Registration of local client failed<br>3: Creation in progress (local client)<br>4: Creation successful (local client)<br>5: Registration of local client successful |
| status               | string | Number status. Enum values: PENDING, DELETED, MIGRATED, BANNED, RESTRICTED, RATE_LIMITED, FLAGGED, CONNECTED, DISCONNECTED, UNKNOWN, UNVERIFIED |
| current_limit        | string | Merchant-initiated session 24-hour limit level. Enum values: TIER_1K: 1,000 customers/24 hours; TIER_10K: 10,000 customers/24 hours; TIER_100K: 100,000 customers/24 hours; TIER_50: 50 customers/24 hours; TIER_250: 250 customers/24 hours; TIER_UNLIMITED: Not applicable |
| code_verification_status | string | Number verification status. Enum values: NOT_VERIFIED: Not verified; VERIFIED: Verified |
| waba_id| string | WABA unique ID |
| waba_name| string | WABA name |

## Response Example
### Successful Example
```json
{
  "code": 0,
  "data": [
    {
      "display_phone_number": "+86 xxx 24",
      "quality_rating": "GREEN",
      "name_status": "APPROVED",
      "verified_name": "GLORY JACK",
      "code_verification_status": "VERIFIED",
      "current_limit": "",
      "register_status": 1,
      "status": "CONNECTED",
      "waba_id": "11696xxxxx86404",
      "waba_name": "GLORY TEST"
    },
    {
      "display_phone_number": "+1 xxx99",
      "quality_rating": "GREEN",
      "name_status": "APPROVED",
      "verified_name": "Glory HK",
      "code_verification_status": "NOT_VERIFIED",
      "current_limit": "",
      "register_status": 1,
      "status": "CONNECTED",
      "waba_id": "11696xxxxx86404",
      "waba_name": "GLORY TEST"
    }
  ],
  "message": "Request successful"
}
```

### Failed Example
```json
{
    "code": -1,
    "message": "Request failed",
    "data": null
}
```

## Response Code Explanation

| code | message           | Solution                    |
| ---- | ----------------- | --------------------------- |
| 0    | Request successful |                             |
| -1   | Request failed    | Please contact technical support to troubleshoot the issue |
| 1000~100X | Authentication issue | Refer to the API authentication section for details |
| 9000 | Parameter exception | Missing parameters, please check the required parameters |
| 9001 | System business error | Please contact technical support to troubleshoot the issue |
| 9007 | Non-integrator request | Please confirm if you are an integrator |
| 9008 | APPKEY does not exist | Please confirm if the APPKEY is correct |
| 9010 | Inconsistent authentication mechanism customer information and APPKEY customer information | Please confirm if the APPKEY is correct |