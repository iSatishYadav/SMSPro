## What is a Webhook

A Webhook is a way for an application to provide information to other applications in real-time.

A Webhook delivers data to other applications as it happens, meaning you get data immediately.

> Unlike typical approaches where you need to poll for the data very frequently in order to get it real-time.

This makes Webhooks much more efficient for both provider and consumer.

## Consuming Webhooks

To get a Webhook callback You need to register your URL, HTTP Method, and other details to the provider.

## Securing a Webhook

As Webhooks deliver data to publicly available endpoints (URLs) in your app, there's a chance that someone else could find that URL and then provide you with false data.

To prevent this from happening, you may implement following:

### 1. Basic Auth

Plain old username an password, which are sent in `Authorization` HTTP header as:

````HTTP
Authorization: Basic base_64_of_username:password
````

### 2. Custom API Key/Shared Key

A custom API key or a pre-shared secret, which can be sent in HTTP body:

````JSON
{
    "param1": "value1",
    "param2": "value2",
    "api-secret": "NGYwMTYyNzEtZGRmYi00YWU1LWI3MDItMmQ3NWVhZDNlNzJj"
}
````

or in a custom Header

````HTTP
Content-Type: application/json
X-API-Secret: ZmRlMTFkMTctYmE1NS00NmE1LTlmZGEtZDI4Y2ZjZmI2MTVj
Accept: application/json
````