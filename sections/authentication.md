Shoeboxed API Authentication
===

All API requests must be authenticated by passing along an OAuth 2.0 token.

By default, Shoeboxed supports the "code grant" which is the standard grant type for apps with a server-side component like web apps. If needed, we can manually enable the "implicit grant" flow for you if you are creating a client-side app such as a mobile app or JS app. Drop us a line at api@team.shoeboxed.com

## Using the code grant

### Step 1: Begin authorization

Direct the user to the OAuth 2.0 authorization endpoint:

    https://api.shoeboxed.com/login/oauth/authorize?client_id=<your client id>&response_type=code&redirect_uri=<your site>&state=<CSRF token>
    
We strongly recommend you use the state parameter to prevent cross-site request forgery (CSRF). You should generate a random CSRF token, store a copy in user's session, then verify it (see below) to prevent forgery.

Once the user has authorized your app, they’ll be sent to your redirect URI, with a few query parameters:

    https://www.yoursite.com/page?code=<authorization code>&state=<CSRF token>

Your app should verify the CSRF token matches the one you previously generated and stored, and then pull out the authorization code which you'll need in the next step.


### Step 2: Obtain an access token




