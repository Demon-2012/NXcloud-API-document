Most of the interfaces in [NXcloud](https://www.nxcloud.com) are submitted in this way.

* Set the HTTP method to `POST`:
```java
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("POST");
```

* Add the `Content-Type: application/x-www-form-urlencoded` header:
```java
connection.setRequestProperty("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8");
```

* Please make sure to correctly urlencode the submitted fields:
```java
String body = "phone=8411111111&content=" + URLEncoder.encode("Your SMS content, Your short link content", "UTF-8") + "&.....";
```

Here is an example screenshot of a submission using Postman:

![Postman Example Screenshot](https://raw.githubusercontent.com/nxtele/http-api-document/main/600e301a94912.png)