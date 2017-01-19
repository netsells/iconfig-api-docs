---
title: API Reference

language_tabs:
  - shell: curl
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

```shell
curl -H "Content-Type: application/json" -X POST \
-d '{"grant_type":"personal_access","client_id":"XXXXX", "client_secret": "XXXXX"}' \
https://api.iconfig.io/oauth/token
```

```php
use Netsells\iConfig\iConfig;

$iConfig = new iConfig($clientId, $clientSecret);
```

To authenticate with iConfig you will need the client ID and secret given to you (these form your account's personal access token). You will need to use these details to obtain an access_token, this token will be used for all future requests.

<aside class="notice">
Make sure to replace the `client_id` and `client_secret` with your details
</aside>
