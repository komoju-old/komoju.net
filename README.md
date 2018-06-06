# Komoju C# Example


```C#
// Creating a payment using JSON API
// See https://docs.komoju.com/api/overview#payments

using System;
using System.IO;
using System.Net;
using System.Text;
using System.Collections.Specialized;

public class HelloWorld
{
    static public void Main ()
    {
        string url = @"https://komoju.com/api/v1/payments";
        WebClient client = new WebClient();
        # set private key of your komoju account as username. 
        String username = "<YOUR_KOMOJU_ACCOUNT_PRIVATE_KEY>";
        String password = "";

        string credentials = Convert.ToBase64String(Encoding.ASCII.GetBytes(username + ":" + password));
        client.Headers[HttpRequestHeader.Authorization] = string.Format("Basic {0}", credentials);
        client.Headers[HttpRequestHeader.ContentType] = "application/x-www-form-urlencoded";

        NameValueCollection myParameters = new NameValueCollection();
        myParameters.Add("amount", "1000");
        myParameters.Add("tax", "0");
        myParameters.Add("currency", "JPY");
        myParameters.Add("payment_details[type]", "credit_card");
        myParameters.Add("payment_details[given_name]", "Taro");
        myParameters.Add("payment_details[family_name]", "Yamada");
        myParameters.Add("payment_details[month]", "01");
        myParameters.Add("payment_details[number]", "4111111111111111");
        myParameters.Add("payment_details[year]", "2016");
        myParameters.Add("payment_details[verification_value]", "123");

        byte[] responseBytes = client.UploadValues(url, "POST", myParameters);
        string responseBody = Encoding.UTF8.GetString(responseBytes);
        Console.WriteLine(responseBody);
    }
}
```
