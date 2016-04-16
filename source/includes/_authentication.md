# Authentication

> To authenticate, add your API key to the HTTP header:

```shell
  curl http://fo-api.dev/v2/mrr/201602 \
  -H 'Authorization: Token token="YourTokenHere"'
  
  
  curl http://fo-api.dev/v2/mrr/201602 \
  -u YourTokenHere:
```

> When using `-u`, remember to add `:` at the end to prevent the password query.

Authenticate your account when using the API by including your secret API key in the request.

You can manage your API keys in FirstOfficer's <a href='https://www.firstofficer.io/api_key'>Authentication Key Generator</a>.
Be sure to keep them secret. Do not share your secret API keys in GitHub, client-side code, and so forth.

All API requests must be made over HTTPS. Calls made over plain HTTP will fail. API requests without authentication will also fail.

<aside class="notice">
You must replace <code>YourTokenHere</code> with your personal API key.
</aside>