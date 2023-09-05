**Brief Description:**

Wake up NXPHONE to make automatic phone calls by creating links for customer's own system phone numbers.

**Invocation Method:**

`<a href="sip:phone,orderid">phone number</a>`

**Invocation Example:**

```
<a href="sip:8888888,xxx123">8888888</a>
```

**Parameters:**

| Parameter | Parameter Name | Required | Type   | Description                                      |
|:----------|:---------------|:---------|:-------|:-------------------------------------------------|
| phone     | Called number  | Yes      | string | Real phone number to be dialed by the system     |
| orderid   | Order ID       | Yes      | string | Unique order ID assigned by the system. Length should be greater than 4 and less than 32, a combination of numbers and letters |
| phone number | Phone number | No       | string | Anchor point for creating the link                |

**Note:**
Developers create links in their own systems, and users can directly click the link to invoke NXPHONE for automatic phone calls. The order ID can be used for call record association through CDR callback interface or CDR query interface.