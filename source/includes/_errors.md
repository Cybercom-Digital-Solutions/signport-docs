# Errors

<aside class="notice">The meaning of error code may differ a bit between different services</aside>

The Kittn API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Something is wrong with your request.
401 | Unauthorized -- Something is wrong with your API key.
403 | Forbidden -- You don't have access to this endpoint.
404 | Not Found -- The specified document/signer could not be found.
405 | Method Not Allowed -- You tried to access the endpoint with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The requested resource has been removed from the server.
418 | I'm a teapot.
500 | Internal Server Error -- We have a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
