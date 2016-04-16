# Errors


> Error Types

```shell
invalid_request_error -- Your request has invalid parameters.

```

> Example of error response

```json
{
  "error": {
    "type": "invalid_request_error",
    "message": "Invalid API Key provided."
  }
}

```

FirstOfficer uses conventional HTTP response codes to indicate the success or failure of an API request.

Error Code | Meaning
---------- | -------
200 | OK -- Everything worked as expected.
401 | Unauthorized -- No valid API key provided.
