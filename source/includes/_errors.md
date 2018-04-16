# <a name="HTTP"></a> Error Codes 

The Graze API returns the following HTTP status and error codes:

Code | Meaning
---------- | -------
200 | Success - Your request was sucessful.
400 | Bad Request - Your request is invalid/incorrectly formatted.
401 | Unauthorized - Your request has an invalid auth_code or user credentials.
403 | Forbidden - Your request is forbidden or is hidden for administrators only.
404 | Not Found - The specified request could not be found.
500 | Failed Request - Your request failed. For example, this might occur if the sitn_id was invalid.
