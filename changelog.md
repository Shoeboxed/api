Changelog
=========

When we delete or rename fields, we strive to support both old and new field names for 30 days.

We will email all developers whenever there are potentially breaking changes. We will send an email to the email address associated with your developer Shoeboxed account. Note: If you have opted out of our communications, you won't get an email update.

## August 7, 2014

With the implementation of a single sign-on service, OAuth2 base URLs have
changed from `https://api.shoeboxed.com/login/` to `https://id.shoeboxed.com/`.
The old URL will be supported in parallel for one month, until September 7;
afterwards, requests to it will return a 301 redirect to the new URL.

We recommend that you change your OAuth2 base URL as soon as possible. Any paths
under the base URL do not change; e.g. `https://api.shoeboxed.com/login/oauth/authorize`
is now `https://id.shoeboxed.com/oauth/authorize`.

Note that the URL for actual API calls do not change; the base URL for that is
still `https://api.shoeboxed.com/v2/`. The only thing that changed is the endpoint
for the OAuth2 process.

June 20, 2014
-------------

After August 10th, backwards compatibility for old property names will be removed. 

1. Deleted Properties

   Please remove usage of the following properties:
     1. collectOriginalCurrency from /accounts/:account/settings
     1. homePhone, all occurrences (not actually removed, but please update usage)
2. Renamed[*]:

   Adjust names for the following properties:

     1. "firstName" becomes "name" and "lastName" becomes "surname" (for all requests and responses). 
        
        // The rationale behind this is that the old names are regional. Some cultures (e.g., Hungary) have different conventions for first and last when it comes to names. "name" and "surname" are somewhat agnostic.

     1. All occurrences of "workPhone" have been renamed to "phone". It's used in the structure of business card and user profile objects.

     1. The "paymentType" enum value "card" has been replaced by "credit-card" in an attempt to keep things consistent 

       The endpoint that used "card" (in both requests and responses) was /accounts/:account/documents.
  
       For example, this:
        ````
        {
          "paymentType": {
            "type": "card",
            "lastFourDigits": "0123"
          }
        }
        ````
      
          becomes this:
       
        ````
        {
          "paymentType": {
            "type": "credit-card",
            "lastFourDigits": "0123"
          }
        }
        ````
  
