# Errors

The Cranson API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request sucks
401 | Unauthorized -- Your API key is wrong
403 | Forbidden -- The plan requested is hidden for administrators only
404 | Not Found -- The specified plan could not be found
405 | Method Not Allowed -- You tried to access a plan with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The plan requested has been removed from our servers
418 | I'm a teapot
429 | Too Many Requests -- You're requesting too many plans! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
