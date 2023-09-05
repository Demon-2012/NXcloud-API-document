**Brief Description:**

- API for uploading voice broadcast audio files.

**Request Method:**
- URL: `http://api2.nxcloud.com/api/voiceSms/uploadVoiceFile`
- Method: `POST`
- Content-Type: `application/x-www-form-urlencoded`

**Parameters:**

| Parameter  | Required | Type   | Description                            |
|:-----------|:---------|:-------|:---------------------------------------|
| appkey     | Yes      | string | App key for the voice application.      |
| secretkey  | Yes      | string | Secret key for the voice application.   |
| filename   | Yes      | string | File name.                             |
| content    | Yes      | string | Base64-encoded file content.            |

**Request Example:**
```shell
curl --location --request POST 'http://api2.nxcloud.com/api/voiceSms/uploadVoiceFile' \
--data-urlencode 'appkey=asdf' \
--data-urlencode 'secretkey=qwer' \
--data-urlencode 'filename=abc.txt' \
--data-urlencode 'content=qwertyuiopasdfghjkl'
```

**Response Example:**
``` 
{
    "code": "success",
    "info":"http://xxxx.xxx/xxxx.mp3"
}
```
``` 
{
    "code": "102",
    "result":"The current account or the account of the agent has been disabled."
}
```

**Response Parameter Description:**

| Parameter | Type   | Description                                      |
|:----------|:-------|:-------------------------------------------------|
| code      | string | success: Request succeeded, others: Request failed. |
| info      | string | URL of the uploaded audio file if the upload is successful. |
| result    | string | Failure result description.                       |

**Note:**

- Example code for Base64 encoding conversion:
```
package com;

import cn.hutool.core.codec.Base64;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class Test {

    public static void main(String[] args) {
        File f = new File("c:\\tmp\\2.m4a");
        System.out.println(file2Base64(f));
    }

    public static String file2Base64(File file) {
        if(file==null) {
            return null;
        }
        String base64 = null;
        FileInputStream fin = null;
        try {
            fin = new FileInputStream(file);
            byte[] buff = new byte[fin.available()];
            fin.read(buff);
            base64 = Base64.encode(buff);
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if (fin != null) {
                try {
                    fin.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
        return base64;
    }
}
```