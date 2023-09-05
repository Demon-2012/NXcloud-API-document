C# request SMS sending interface sample code, please refer to

```csharp
using System;
using System.Net;
using System.Text;
using System.IO;
using System.Collections.Generic;
using System.Web.Script.Serialization;

namespace nxcloud
{
    public class NxCloud
    {
        // Note: content needs to be URL-encoded using HttpUtility.UrlEncode
        public static String send(String phone, String content, String appkey, String secretkey)
        {
            Encoding myEncoding = Encoding.GetEncoding("UTF-8");  // Select encoding character set
            string data = "appkey=" + appkey + "&secretkey=" + secretkey + "&phone=" + phone + "&content=" + content;
            byte[] bytesToPost = System.Text.Encoding.Default.GetBytes(data); // Convert to bytes data

            string responseResult = String.Empty;
            HttpWebRequest req = (HttpWebRequest)HttpWebRequest.Create("http://api.nxcloud.com/api/sms/mtsend");
            req.Method = "POST";
            req.ContentType = "application/x-www-form-urlencoded;charset=UTF-8";
            req.ContentLength = bytesToPost.Length;

            using (Stream reqStream = req.GetRequestStream())
            {
                reqStream.Write(bytesToPost, 0, bytesToPost.Length);
            }
            HttpWebResponse cnblogsRespone = (HttpWebResponse)req.GetResponse();
            if (cnblogsRespone != null && cnblogsRespone.StatusCode == HttpStatusCode.OK)
            {
                StreamReader sr;
                using (sr = new StreamReader(cnblogsRespone.GetResponseStream()))
                {
                    responseResult = sr.ReadToEnd();
                }
                sr.Close();
            }
            cnblogsRespone.Close();

            JavaScriptSerializer serializer = new JavaScriptSerializer();
            Dictionary<string, object> json = (Dictionary<string, object>)serializer.DeserializeObject(responseResult);

            Console.WriteLine(responseResult);
            return (String)json["messageid"];
        }

        public static void Main(string[] args)
        {
            NxCloud.send("", "", "", "");
            Console.Read();
        }
    }
}
```