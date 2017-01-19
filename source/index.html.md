---
title: API Reference

language_tabs:
  - http
  - php

toc_footers:
  - <a href=''>Contact Support</a>

includes:
  # - errors

search: true
---

# API Reference

The iConfig API is mostly REST based. We make use of HTTP response codes and standards based authentication.

At the moment we offer an SDK for the API in php only. You can view the SDK languages using the selector at the top right.

# Authentication

```http
POST /oauth/token HTTP/1.1
Accept: application/json
Host: api.iconfig.io
Content-Type: application/json

{"grant_type":"personal_access", "client_id":"XXXXX", "client_secret": "XXXXX"}
```

```php
use Netsells\iConfig\iConfig;

$iConfig = new iConfig($clientId, $clientSecret);
```

To authenticate with iConfig you will need the client ID and secret given to you (these form your account's personal access token). You will need to use these details to obtain an access_token, this token will be used for all future requests.

<aside class="notice">
Make sure to replace the `client_id` and `client_secret` with your details
</aside>
