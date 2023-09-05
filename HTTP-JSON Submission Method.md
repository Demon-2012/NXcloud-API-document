Some of the interfaces in [NXcloud](https://www.nxcloud.com) are submitted in this way.

* Set the HTTP method to `POST`:
```java
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("POST");
```

* Add the `Content-Type: application/json` header:
```java
connection.setRequestProperty("Content-Type", "application/json; charset=UTF-8");
```