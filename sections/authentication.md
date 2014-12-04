Shoeboxed API Authentication
===

All API requests must be authenticated by passing along an OAuth 2.0 token.

Shoeboxed supports two Oauth 2.0 grant types:
  - the "code grant" which is the standard grant type for apps with a server-side component like web apps.
  - the "implicit grant" flow for you if you are creating a client-side app such as a mobile app or browser extension

We can enable other Oauth 2 grant types upon request. Please email api@team.shoeboxed.com

## Using the code grant

### Step 1: Begin authorization

Direct the user to the OAuth 2.0 authorization endpoint:

    https://id.shoeboxed.com/oauth/authorize?client_id=<your client id>&response_type=code&scope=all&redirect_uri=<your site>&state=<CSRF token>
    
We strongly recommend you use the state parameter to prevent cross-site request forgery (CSRF). You should generate a random CSRF token, store a copy in user's session, then verify it (see below) to prevent forgery.

Once the user has authorized your app, they’ll be sent to your redirect URI, with a few query parameters:

    https://www.yoursite.com/page?code=<authorization code>&state=<CSRF token>

Your app should verify the CSRF token matches the one you previously generated and stored, and then pull out the authorization code which you'll need in the next step.


### Step 2: Obtain an access token

To exchange the authorization code for an access token, you need to do a server-side POST to the /token endpoint:

```bash
$ curl -v -XPOST https://id.shoeboxed.com/oauth/token \
    -d code=<authorization code> \
    -d grant_type=authorization_code \
    --data-urlencode redirect_uri='<your site>' \
    -u <your client id>:<your client secret>
```

The response will look like:

```json
{
  "access_token": "1cb04374-da51-4394-adaf-ae7d4ee05571",
  "refresh_token": "b162991a-d3e0-4509-a86c-8dcd3f624475",
  "token_type": "bearer",
  "expires_in": 1800, // in seconds
  "scope": "all"
}
```

Access tokens are short-lived, in keeping with OAuth2 best practices. It is a
good idea to persist the refresh token so that you can renew your access token
later.

### Step 2a: Using a refresh token to get a new access token

```bash
$ curl -v -XPOST https://id.shoeboxed.com/oauth/token \
    -d grant_type=refresh_token \
    -d client_id=<your client id> \
    -d client_secret=<your client secret> \
    -d refresh_token=<your refresh token>
```

You will get a response like:

```json
{
    "access_token": "e1a7470d-4e10-4cfc-87c6-08464b0a5fc2",
    "expires_in": 1800,
    "scope": "all",
    "token_type": "bearer"
}
```

### Step 3: Call the API

Now that you have an access token, you can call any method in the v2 API by just attaching the following header:

    Authorization: Bearer <access token>

As an example, here's how to use curl to get information about the user:

    curl https://api.shoeboxed.com/v2/user -X GET -H 'Authorization: Bearer <user access token>'
