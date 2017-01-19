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

{
    "grant_type":"personal_access", 
    "client_id":"XXXXX", 
    "client_secret": "XXXXX"
}
```

```php
$iConfig = new Netsells\iConfig\iConfig($clientId, $clientSecret);
```

To authenticate with iConfig you will need the client ID and secret given to you (these form your account's personal access token). You will need to use these details to obtain an access_token, this token will be used for all future requests.

<aside class="notice">
Make sure to replace the `client_id` and `client_secret` with your details
</aside>

# Configs
The heart of iconfig. We currently only offer email configuration but have allowed scope for future configs.

## Create Config

```http
POST /config/create HTTP/1.1
Accept: application/json
Host: api.iconfig.io
Content-Type: application/json

{
  "configs": {
    "email": [
      {
        "email_address": "my@email.com",
        "EmailAccountType": "EmailTypeIMAP",
        "IncomingMailServerAuthentication": "EmailAuthPassword",
        "OutgoingMailServerAuthentication": "EmailAuthPassword",
        "IncomingPassword": "mysecureemailpassword",
        "OutgoingPassword": "mysecureemailpassword",
        "IncomingMailServerHostName": "mail.email.com",
        "OutgoingMailServerHostName": "mail.email.com",
        "IncomingMailServerPortNumber": "993",
        "OutgoingMailServerPortNumber": "587",
        "IncomingMailServerUseSSL": true,
        "OutgoingMailServerUseSSL": true
      }
    ]
  },
  "settings": {
    "password": "mysecurepassword"
  }
}
```

```php
<?php

use Netsells\iConfig\Email;

$config = new Netsells\iConfig\Config;

// Configure Settings
$settings = new Netsells\iConfig\ConfigSettings;
$settings->setPassword('mysecurepassword');

$config->setSettings($settings);

// Configure Email
$emailConfig = new Email;
$emailConfig->setEmailAddress('my@email.com');
$emailConfig->setEmailAccountName('Testy McEmailface');

$emailConfig->setType(Email::TYPE_IMAP);

$emailConfig->setIncomingAuthentication(Email::AUTHENTICATION_PASSWORD);
$emailConfig->setOutgoingAuthentication(Email::AUTHENTICATION_PASSWORD);

$emailConfig->setIncomingUsername('my@email.com');
$emailConfig->setOutgoingUsername('my@email.com');

$emailConfig->setIncomingPassword('mysecureemailpassword');
$emailConfig->setOutgoingPassword('mysecureemailpassword');

$emailConfig->setIncomingPort(993);
$emailConfig->setOutgoingPort(465);

$emailConfig->setIncomingServerSSL(true);
$emailConfig->setOutgoingServerSSL(true);

$emailConfig->setIncomingServer('mail.email.com');
$emailConfig->setOutgoingServer('mail.email.com');

$config->addPayload($emailConfig);

// Send the Config
$response = $iConfig->submitConfig($config);
```

Our SDK library allows you to create the config in an OOP way. You can see examples to the right.
