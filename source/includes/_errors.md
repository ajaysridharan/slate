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
400 | Bad Request -- The request was unacceptable, often due to missing or invalid parameter.
401 | Unauthorized -- No valid API key provided.
404 | Not Found -- The requested object does not exist.

Error Attributes

Attribute | Description
---------- | -------
type | The type of the error. Can be: "invalid_request_error"
message | A human-readable message providing more details about the error.
param | The parameter this error relates to. Optional.
