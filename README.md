# Shoeboxed Api v2

The Shoeboxed v2 API empowers anyone to:
  + securely integrate Shoeboxed user data seamlessly into your web, mobile or desktop application
  + extend Shoeboxed's core functionality
  + leverage Shoeboxed's receipt data and/or OCR for your product
  + whitelabel or build on top of our receipt and document processing system (some business conditions apply)
  + create new ways for Shoeboxed users to add receipts, business cards, or documents
  + .. and much more!

## Beta

This API is currently in public beta, which means endpoints may change without notice. 

Please 'Watch' this GitHub repository so that you're automatically notified when this documentation is updated.

## Is this API Production ready?

We are currently using it in production for the following Shoeboxed services:

  + Gmail Receipt Sync
  + All new user registration
  + In all new screens in our web application, including:
    + Web-based receipt & document uploader
    + Account Settings
    + User Settings
    + New Receipt Tables
  + (expected June 2014) relaunched iOS 7 app
  + Shoeboxed Web Clipper

# Oauth 2

We use OAuth 2 to authenticate all API requests. To get started, generate an OAuth 2.0 client_id and client_secret for your app:

1. Sign up for Shoeboxed if you don't have an account
    + **A paid Shoeboxed account is not required**
    + Sign up for Shoeboxed [here](https://register.shoeboxed.com/). **Tip:** _For a free DIY account, click the 'Maybe Later' button when you reach the pricing page_
2. [Generate Your OAuth 2 Credentials](https://app.shoeboxed.com/member/v2/user-settings#api) Once finished, be sure to copy your client_id and client_secret.

Now that you have your own credentials, you may either:
  + use any OAuth 2.0 client library to authenticate requests to our API [View OAuth Urls and Supported Grant Types](sections/authentication.md)
  + or, manually run through the OAuth 2.0 flow [View Step-by-Step Guide](sections/authentication.md) 

If you want to get started quickly making calls against our API, check out [Step-by-Step OAuth 2.0 Guide](sections/authentication.md) 

# API Endpoints

Our [Swagger](https://helloreverb.com/developers/swagger) documentation is the most complete description of all endpoints and parameters. If you plug in your OAuth credentials, you may make test calls to the API without leaving your browser.

[Browse Shoeboxed v2 API Endpoints](https://api.shoeboxed.com/v2/explorer/index.html)


# Support

Feature requests? Bugs? Please file a Github issue.

We are also available over email: api@team.shoeboxed.com


## Legacy (v1) API Support

Warning: A .zip archive of the old, legacy API docs is provided for *existing* users of the legacy API. We strongly recommend you migrate to API v2 as soon as possible. Please email us at api@team.shoeboxed.com with any questions or concerns. [OLD API docs archive. Right Click to Download.](sections/legacy-v1-api-documentation.zip)
