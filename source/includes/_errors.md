# Errors

<aside class="notice">
This will have to change and become more specific to the request as the API develops. This is a general overview of what should be returned upon error.
</aside>

The BCX Data API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- That information is hidden for administrators only.
404 | Not Found -- The specified item could not be found.
405 | Method Not Allowed -- You tried to access data with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json or csv.
410 | Gone -- The object requested has been removed from our servers.
429 | Too Many Requests -- You're requesting too many things too quickly. Slow down.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
