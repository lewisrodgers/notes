# Google APIs, OAuth 2, and Postman

https://developers.google.com/explorer-help/

Note to self: I believe that you cannot use the explorer to make requests for certain methods. For the `calendars.clear` method, it seems that you have to be logged in as the user in order to be able to clear the calendar. 

In other words, in order to clear the calendar for `michael.scott@dunder.com` you'd need to log in as Michael Scott.

A service account (wit DwD) can impersonate Micheal Scott — effectively logging in as Micheal Scott.

In code, the service account calls the `clear` method as the user that owns the calendar. In contrast, if I call the `clear` method from the explorer — even as someone with admin priveledges — I can only call the method as myself. Which means I can only clear the calendar that I own. In general, methods like `clear` can only executed for other users other than youself, in code with a service account. (I'm still trying to verify this)

You'll get an error response like below:

If you don't provide a client ID to the explorer, you'll get a 401.

> 401: This method requires you to be authenticated. You may need to activate the toggle above to authorize your request using OAuth 2.0.

```json
{
 "error": {
  "errors": [
   {
    "domain": "global",
    "reason": "required",
    "message": "Login Required",
    "locationType": "header",
    "location": "Authorization"
   }
  ],
  "code": 401,
  "message": "Login Required"
 }
}
```

If you provide both an API key and client ID, and get a 403, then this probably means you need to use this method in code with a service account and DwD.

> 403: You do not have permission to execute this method.

```json
{
 "error": {
  "errors": [
   {
    "domain": "global",
    "reason": "forbidden",
    "message": "Forbidden"
   }
  ],
  "code": 403,
  "message": "Forbidden"
 }
}
```