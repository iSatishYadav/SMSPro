# Hello Developers
This is a quick guide on how to get started on BPCL’s Enterprise SMS API called _SMSPro_.

_SMS Pro_ uses industry standard _OAuth2_ for authentication. We’ll not talk about OAuth here as it’s out of scope of this document.

However, rest assured all major API Vendors e.g. Google, Facebook, Twitter, Instagram etc. use _OAuth2_ for their APIs.

_SMS Pro_ uses _Client Credentials_ grant type of OAuth among many others.

## 1. Registration
Before you call SMS Pro API, you need to register your application [here][Link: Application Registration]. Register and come back here.

Once you’ve registered your application, you’ll get `client_id` and `client_secret`.
`client id` is a uniuqe identifier for your application and `client_secret` is like a password, DO NOT SHARE IT WITH ANYONE.

## 2. Calling API
If you're using .NET check our [SMS Pro Client SDK (.NET)][Link: .NET Client SDK]​, which sends SMS in just one line of code.

Or continue...​

So, there are 2 steps to call _SMS Pro_ API.

1. Getting Access Token.
2. Using Token to call SMS API.​

For code samples, see [Calling SMS Pro API: Code Samples][Link: Code Samples]​.

## 2.1 Getting Access Token
Send A `POST` request to [/oauth2/token][Endpoint: OAuth2 Token] endpoint for getting an _OAuth2_ token.

### 2.1.1 Request
A typical request looks like this:

````http
POST .../oauth2/token HTTP/1.1
Host: SMS Pro API URL
Content-Type: application/x-www-form-urlencoded

client_id=1234&client_secret=12345&grant_type=client_credentials
````
> Content-Type: `application/x-www-form-urlencoded` requires values to be URL-Encoded and then passed to the API.

### 2.1.2 Response
For which the `JSON` response will look like this:
````json
{
  "access_token": "faXvojWzmCbCxNhdwv...", --Shortedned for brevity
  "token_type": "bearer",
  "expires_in": 3599
}
````
This is `bearer` type token, The token also contains an `expires_in` parameter, which tell for how many seconds this token in valid and can be used.
In this case it’s 3599 seconds i.e. ~60 minutes.

Take this `access_token` which will be used to access protected resource, in this case SMS Pro API

## 2.2 Using Token to call SMS API
Send a `POST` request to [/api/SMS][Endpoint: SMS API] endpoint.
There are 2 parameters `Mobile` and `Message`. For validations see section 3 of this document.

### 2.2.1 Request
Your request may look like this.

````HTTP
POST .../​​api/SMS HTTP/1.1
Host: localhost:1472
Authorization: Bearer NJzhrzHTzZ_oJh7XK0i-l9VnEh-1_ssW... --Shortened for brevity
Content-Type: application/x-www-form-urlencoded

Mobile=9167005157&Message=Hi%2C+Satish+Yadav!+This+is+a+demo+SMS+from+BPCL+SMS+Pro.
````

> You can also send `JSON` payload with `Content-Type` header as `appplication/json`

### 2.2.2 Response
If everything goes okay, you’ll get an `HTTP 204 (No Content)` or `HTTP 202 (Accepted)` HTTP Response.

If any validation fails, you’ll get `HTTP 400 (Bad Request)`. Read section 3 for more about validations.


## 3. Validations
Following are the basic validation.

 Parameter     | Required?     | Validation(s)               
 ------------- |-------------- | --------------------------- 
 Mobile        | Yes           |  10 Digit ( Valid Indian Mobile  number) 
 Message       | Yes           |  160 characters (Max)      

## 3.1 Error Messages

In case any validation fails, you’ll get an HTTP 400 (Bad Request).

e.g. If you send invalid `Mobile` and message with more than 160 characters, You’ll get response like this:

````json
{
  "Message": "The request is invalid.",
  "ModelState": {
    "sms.Mobile": [
      "Mobile should be a valid Indian mobile number."
    ],
    "sms.Message": [
      "Message can only be 160 characters."
    ]
  }
}
````
That’s all! Happy Coding!

[Link: Application Registration]:https://testmy.ebharatgas.com/SmsPortal/Applications/Create?utm_source=Docs&utm_medium=Prod
[Link: .NET Client SDK]:http://myspace.iconnect.com/my/satishkyadav/Sms/SMS%20Pro%20Client%20SDK%20C/Home.aspx?utm_source=Docs&utm_medium=Prod
[Link: Code Samples]:http://myspace.iconnect.com/my/satishkyadav/Sms/_layouts/15/start.aspx#/SMS%20Pro%20Code%20Samples/Home.aspx?utm_source=Docs&utm_medium=Prod

[Endpoint: OAuth2 Token]: https://testmy.ebharatgas.com/SMS/oauth2/token

[Endpoint: SMS API]: https://testmy.ebharatgas.com/SMS/api/SMS
