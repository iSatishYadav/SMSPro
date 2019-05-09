## Webhook Registration
Webhook is a modern way of efficiently sending data from a producer app to a consumer app in real-time in an event-driven architecture.

If you'd like to read more about Webhooks [click here][Link: What is a Webhook] and come back.

### Registering Webhook

Visit [SMS Pro Portal Application Registration (PULL)][Link: Application Registration] Page and fill in details:

1. _Webhook Name_: An easy to remember webhook name.
2. _Url_: URL at which the Webhook will be pushed.
3. _Method_: Choose either HTTP `GET` or `POST`
4. _Query Strings_: Any query string required to be sent with the Webhook payload.
5. _Headers_: Any HTTP header required in your appplication with the Webhook payload. e.g `Content-Type: application/json` or `Authorization: Basic malkjafjasdl_asdfjHSIFEUN`
6. "_Body_": HTTP Body as per your requirement in your application.

> You must use `@@mobile@@` and `@@message@@` placeholders in either _Body_, _Header_, or _Query String_. These will be replaced by consumer's mobile and message sent, respectively.

Webhook Registration:

![webhook registration][Link: Image: Webhook Registration]


### Webhook Flow

As soon as user sends an SMS, the registered endpoint will be sent payload with specified HTTP details.

### Retries and Success

If the response is `HTTP 200`, the webhook is considers as success, otherwise it'll be retried 10 times exponentially.

[Link: Application Registration]:https://testmy.ebharatgas.com/SmsPortal/WebhookRegistration/Create?utm_source=Docs&utm_medium=Dev

[Link: What is a Webhook]:../webhook
[Link: Image: Webhook Registration]: ../images/webhook-registration.png