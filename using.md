---
title: The use.thiss.io demo service
permalink: /use/
layout: page
---

The [use.thiss.io](https://use.thiss.io) is a demo install of the thiss-js software provided on a best-effort basis for service providers who want to experiment with the discovery service without having to install their own instance. 

There are two ways to use the service:

1. Use as a regular "classic" SAML discovery service.
2. Use the active login button

In order to do this configure your SP to use https://use.thiss.io/ds/ as the discovery service URL.  In addition to using use.thiss.io as a regular discovery service you can configure your SP to use the active login button. Exactly how you do this depends on your SAML SP software initializes login flows. If you use Shibboleth you can include the following JS on the login page:

```
<script src="https://use.thiss.io/thiss.js"/>
<div id="login"/>
<script>
    window.onload = function() {
       thiss.DiscoveryComponent.render({
           loginInitiatorURL: 'https://sp.example.com/Shibboleth.sso/Login?target=https://sp.example.com/service',
       }, '#login');
    };
</script>
```

In this example "/Shibboleth.sso/Login" is the login context configured in shibboleth2.xml associated with the use.thiss.io discovery service and sp.example.org is your SPs public URL. For an example of how this looks visit [use.thiss.io](https://use.thiss.io/).
