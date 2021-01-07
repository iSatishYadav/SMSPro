# ​SMSPro Client SDK​ (.NET​) 
You can use **SMSPro​ Client SDK** to send SMS in your `.NETapplications`. **SDK** will do all the heavy lifting of calling `REST` endpoints, handling errors, managing `tokens` etc.

## Usage
### 1. Install Nuget Package
Install [Bpcl.SmsPro.Client package][1].

### 2. Using SMSPro Client SDK
Using **SMSPro Client SDK** is literally a one liner. See:

### 2.1 Code Sample
````csharp
await new SmsProClient("https://<SERVER_NAME>/SMS/", "<Client Id>", "Client Secret").SendAsync("<Message>", "<Mobile>");
````

### 2.2 [Optional] Code Sample with Logger
You can pass an `Acion<string>` which will be called throughout the process of sending SMS.

````csharp
public void Logger(string message)
{
    //TODO: Log messages to some log or Console for tesitng.
    Console.WriteLine(message);
}
//...
var client = new SmsProClient("https://<SERVER_NAME>/SMS/", "<Client Id here>", "Client Secret here", Logger);
await client.SendAsync("<Message>", "Mobile");
````

### 3. Exceptions
**SMS Pro Client SDK** will raise `ArgumentException` and `ArgumentNullException` in case of any value is null or empty also when `client_id` and/or `client_secret` is/are invalid.
>So you should `try` to `catch` any `Exception` that might be raised by `SDK`.

Happy Coding!​

[1]: https://www.nuget.org/packages/Bpcl.SmsPro.Client
