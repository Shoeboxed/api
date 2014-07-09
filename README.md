# Shoeboxed Api v2 (beta)

**The new Shoeboxed API is a full-featured RESTful web service that uses OAuth 2.0 for authentication.**

Everything is self-serve: All you need is a free Shoeboxed account to get started!

The Shoeboxed v2 API empowers developers to:
  + securely integrate Shoeboxed user data seamlessly into your web, mobile or desktop application
  + extend Shoeboxed's core functionality
  + leverage Shoeboxed's receipt data and/or OCR for your product
  + whitelabel or build on top of our receipt and document processing system (some business conditions apply)
  + create new ways for Shoeboxed users to add receipts, business cards, or documents
  + .. and much more!

## Libraries

Our API is only offered at this time as a HTTP web service. We do not provide native libraries or wrappers. 

If you write a library for our API, we'd love to add a link! Please email the repo url to api@team.shoeboxed.com

## Is this api production ready?

This API is in **public beta**. In other words, please use at your own risk and absolutely no warranties or guarantees are expressed or implied.

We are 'dogfooding' this API. All new Shoeboxed functionality is built by our developers using this API, so it is in *everyone's* interests to minimize breaking changes.

Shoeboxed is currently using this API in production for the following products and features:

  + Gmail Receipt Sync
  + All new user registration
  + In all new screens in our web application, including:
    + Web-based receipt & document uploader
    + Account Settings
    + User Settings
    + New Receipt Tables
  + (expected June 2014) relaunched iOS 7 app
  + Shoeboxed Web Clipper

We recommend that you 'Watch' this GitHub repository so that you're automatically notified when this documentation is updated.

# Getting Started

## Authentication

We use OAuth 2 to authenticate all API requests. To get started, generate an OAuth 2.0 client_id and client_secret for your app:

1. Sign up for Shoeboxed if you don't have an account
    + **A paid Shoeboxed account is not required**
    + Sign up for Shoeboxed [here](https://register.shoeboxed.com/). **Tip:** _For a free DIY account, click the 'Maybe Later' button when you reach the pricing page_
2. [Generate Your OAuth 2 Credentials](https://app.shoeboxed.com/member/v2/user-settings#api) Once finished, be sure to copy your client_id and client_secret and store them somewhere secure.

Now that you have your own credentials, you may either:
  + use any OAuth 2.0 client library to authenticate requests to our API [View OAuth Urls and Supported Grant Types](sections/authentication.md)
  + or, manually run through the OAuth 2.0 flow [View Step-by-Step Guide](sections/authentication.md) 

If you want to get started as fast as possible making calls against our API, check out [Step-by-Step OAuth 2.0 Guide](sections/authentication.md)

## API endpoints

We use Swagger to provide an interactive API explorer that both documents the functionality of our API and allows you to make test calls directly from your browser. 

[Browse API Endpoints (you will leave GitHub)](https://api.shoeboxed.com/v2/explorer/index.html)

**Tip:** Plug in a valid OAuth access token to make calls to our API from the documentation without leaving your browser.

## Webhook notifications

We provide notifications for documents as they go through Shoeboxed processing.
Fill in a desired notification URL for your [API client](https://app.shoeboxed.com/member/v2/user-settings#api),
and any documents that belong to Shoeboxed users who have granted access to your
application will trigger notifications of its status changes as it moves through
the processing pipeline.

The notifications look like this:

```json
{
    "DocumentId": "5319ef30e4b0aeb0ce0da7b0",
    "Event": "processed",
    "Token": "XWGAsFADpPjHg70GTIvhB7EpoOjsWIduMMoc8j8vhG94bJEAam",
    "Signature": "miUJlR4KROB9GNfDpjIfR1Yje9qNXlK9yPkk4SMHsvU="
}
```

`Event` is one of `created` or `processed`.

`Token` is a 50-character random alphanumeric string; `Signature` is the HMAC
of the token, using SHA-256 as the hash function and your API client secret as
the key, and finally base64-encoded. This serves to verify that the notification
is from Shoeboxed.

An example of computing the signature using the token and client secret using
Python 2.7:

```python
import hashlib, hmac, base64

token = b'provided token here'
secret = b'api client secret here'
signature = base64.b64encode(hmac.new(secret, token, digestmod=hashlib.sha256).digest())
print(signature)
```

Your application that receives the notification must return a status code in the
200s. If it does not, or if we encounter any other network error, then we will
retry the notification up to 10 times, in increasing intervals. The exact times
at which we will retry the notification are `2^n * 90`, where `n` is the number
of retries between 1 and 10; the resulting number is the number of seconds after
the original notification at which we will attempt to retry.

# Support

Feature requests? Bugs? Please file a Github issue.

We are also available over email: api@team.shoeboxed.com

# API Terms of Service

[View API Terms of Service](sections/terms.md)

## Legacy (v1) API Support

Warning: A .zip archive of the old, legacy API docs is provided for *existing* users of the legacy API. We strongly recommend you migrate to API v2 as soon as possible. Please email us at api@team.shoeboxed.com with any questions or concerns. [OLD API docs archive. Right Click to Download.](sections/legacy-v1-api-documentation.zip)
