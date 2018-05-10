# ​Calling SMSPro API: Code Samples
This document contains code samples for calling _SMSPro OAuth2 REST_ API.

## 1. C#
There is a [SMSPro Client SDK (.NET)][Link: .NET Client SDK], you can use that to send SMS in just one line of code. 

Or continue...​

### 1.1 Token

````csharp
var client = new RestClient(".../oauth2/token");

var request = new RestRequest(Method.POST);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/x-www-form-urlencoded");

request.AddParameter("application/x-www-form-urlencoded", "client_id=Your_Token_Here&client_secret=Your_Client_Secret&grant_type=client_credentials", ParameterType.RequestBody);

IRestResponse response = client.Execute(request);
````

### 1.2 POST

````csharp
var client = new RestClient(".../api/SMS");

var request = new RestRequest(Method.POST);

request.AddHeader("cache-control", "no-cache");
request.AddHeader("content-type", "application/x-www-form-urlencoded");
request.AddHeader("authorization", "Bearer Your_Token");

request.AddParameter("application/x-www-form-urlencoded", "Mobile=Your_Mobile_Number&Message=Your_Message_Text", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
````

## 2. JAVA
### 2.1 Token

````java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");
RequestBody body = RequestBody.create(mediaType, "client_id=Your_Client_Here&client_secret=Your_Client_Secret&grant_type=client_credentials");
Request request = new Request.Builder()
  .url(".../oauth2/token")
  .post(body)
  .addHeader("content-type", "application/x-www-form-urlencoded")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
````

### 2.1 POST

````java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/x-www-form-urlencoded");

RequestBody body = RequestBody.create(mediaType, "Mobile=Your_Mobile_Number&Message=Your_Message_Text");

Request request = new Request.Builder()
  .url(".../api/SMS")
  .post(body)
  .addHeader("authorization", "Bearer Your_Token")
  .addHeader("content-type", "application/x-www-form-urlencoded")
  .addHeader("cache-control", "no-cache")
  .build();

Response response = client.newCall(request).execute();
````

## 3. JavaScript
### 3.1 Token

````javascript
var data = "client_id=Your_Client_Here&client_secret=Your_Client_Secret&grant_type=client_credentials";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", ".../oauth2/token");
xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
xhr.setRequestHeader("cache-control", "no-cache");

xhr.send(data);
````

### 3.2 POST

````javascript
var data = "Mobile=Your_Mobile_Number&Message=Your_Message_Text";

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("POST", ".../api/SMS");
xhr.setRequestHeader("authorization", "Bearer Your_Token");
xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
xhr.setRequestHeader("cache-control", "no-cache");

xhr.send(data);
````

## 4. jQuery
### 4.1 Token


````javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": ".../oauth2/token",
  "method": "POST",
  "headers": {
    "content-type": "application/x-www-form-urlencoded",
    "cache-control": "no-cache"
  },
  "data": {
    "client_id": "Your_Client_Id",
    "client_secret": "Your_Client_Secret",
    "grant_type": "client_credentials"
  }
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
````

### 4.2 POST

````javascript
var settings = {
  "async": true,
  "crossDomain": true,
  "url": ".../api/SMS",
  "method": "POST",
  "headers": {
    "authorization": "Bearer Your_Token",
    "content-type": "application/x-www-form-urlencoded",
    "cache-control": "no-cache"
  },
  "data": {
    "Mobile": "Your_Mobile_Number",
    "Message": "Your_Message_Text"
  }
}

$.ajax(settings).done(function (response) {
  console.log(response);
});
````

## 5. Node.js
### 5.1 Token 

````javascript
var request = require("request");

var options = { method: 'POST',
  url: '.../oauth2/token',
  headers: 
   { 'cache-control': 'no-cache',
     'content-type': 'application/x-www-form-urlencoded' },
  form: 
   { client_id: 'Your_Client_Id',
     client_secret: 'Your_Client_Secret',
     grant_type: 'client_credentials' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
````

### 5.2 POST

````javascript
var request = require("request");

var options = { method: 'POST',
  url: '.../api/SMS',
  headers: 
   { 'cache-control': 'no-cache',
     'content-type': 'application/x-www-form-urlencoded',
     authorization: 'Bearer Your_Token' },
  form: { Mobile: 'Your_Mobile_Number', Message: 'Your_Message_Text' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
````

## 6. PHP
### 6.1 Token

````php
<?php

$request = new HttpRequest();
$request->setUrl('.../oauth2/token');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'cache-control' => 'no-cache',
  'content-type' => 'application/x-www-form-urlencoded'
));

$request->setContentType('application/x-www-form-urlencoded');
$request->setPostFields(array(
  'client_id' => 'Your_Client_Id',
  'client_secret' => 'Your_Client_Secret',
  'grant_type' => 'client_credentials'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
````

### 6.2 POST

````php
<?php

$request = new HttpRequest();
$request->setUrl('.../api/SMS');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'cache-control' => 'no-cache',
  'content-type' => 'application/x-www-form-urlencoded',
  'authorization' => 'Bearer Your_Token'
));

$request->setContentType('application/x-www-form-urlencoded');
$request->setPostFields(array(
  'Mobile' => 'Your_Mobile_Number',
  'Message' => 'Your_Message_Text'
));

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}​
````
[Link: .NET Client SDK]: client-sdk