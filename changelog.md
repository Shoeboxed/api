Changelog
=========

When we delete or rename fields, we strive to support both old and new field names for 30 days.

June 20, 2014
-------------

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
  
