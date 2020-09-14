# Errors

<aside class="notice">
API Errors
</aside>

Errors a plugin can request the API to return:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- Your API key doesn´t have permissions to request this.
404 | Not Found -- The specified plugin could not be found.
405 | Method Not Allowed -- You tried to access a plugin with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You run into the maximum requests for a plugin.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
