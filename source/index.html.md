---
title: FirstOfficer API Reference

language_tabs:
  - shell
  - ruby

toc_footers:
  - <a href='https://www.firstofficer.io/api_key'>Generate an Authentication Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - authentication
  - errors
  - customers
  - mrr
  - invoices

search: true
---

# Introduction

```code
API Endpoint

https://api.firstofficer.io
```

> Current version: V2 (BETA, under development)

This API gives you a REST-based access to your SaaS metrics. 
You need a <a href='https://www.firstofficer.io'>FirstOfficer.io</a> subscription to use the API.

JSON is returned by all API responses, including errors.

 

Please note that the API is currently in beta and contents may change. 
V2 will be the first publicly available version and all non-backwards compatible changes will be made to a new API version.
  
At the moment there are not query limits at place, so please use common sense when retrieving data. 
FirstOfficer updates your data once per hour.  
