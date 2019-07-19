---
title: Integration Guide
permalink: /integration/
layout: page
---

The [thiss-js](https://github.com/TheIdentitySelector/thiss-js) software is a complete discovery solution compatible with any MDQ service that implements the search extensions for instance [pyff.io](https://pyff.io) or [thiss-mdq](https://github.com/TheIdentitySelector/thiss-mdq). Regardless of weaather you deploy your own instance of thiss-js or if you connect to an existing service - eg the [use.thiss.io Demo Service](/use/), you need to integrate the instance into your SP. The examples below all assume a SAML SP but it is likely relatively easy to provide a similar solution for OpenIDC or other identity protocols that rely on redirects. 

In the examples below we'll assume you are integrating with use.thiss.io - if you are deploying your own instance of thiss-js, substitute this domain for your own in the various configuration examples below. 

# Integrating a SAML Service Provider

Lets assume you are setting up a SAML SP called sp.example.com. 

The thiss-js software provides several integration options:

 - An implementation of [the SAML identity provider discovery protocol](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-idp-discovery.pdf)
 - A browser-based login button component you can display on your site
 - A jquery plugin for implementing your own discovery service on top of the thiss-js infrastructure

These are presented in order of difficultý. The third option should only be attempted if your SP requires a custom search interface or relies on a non-standard SAML metadata feed but you still want the user to be able to remember their login choice across several SPs.

## Discovery Service Integration

By far the easiest integration is to use thiss-js as a standard SAML identity provider discovery service. The DS url is https://use.thiss.io/ds - just enter this into your SPs configuration where appropriate. Here is how to do this for some common SP sofware stacks:

### Shibboleth

In the file /etc/shibboleth/shibboleth.xml modify the SSO element to read:

```
<SSO discoveryProtocol="SAMLDS" discoveryURL="https://use.thiss.io/ds/">
   SAML2
</SSO>
```

For a complete set of options related to discovery see the [shibboleth documentation](https://wiki.shibboleth.net/confluence/display/SP3/Home).

### SimpleSAMLPhp

In authsources.php (relative to the SSP config directory) find your SAML authentication source (often named 'default-sp') and set the discoURL parameter to https://use.thiss.io/ds/:

```
'default-sp' => array(
    'saml:SP',
    'entityID' => NULL,
    'discoURL' => 'https://use.thiss.io/ds/',
    ....
),
```

For more details visit the [SSP documentation](https://simplesamlphp.org/docs/stable/).

## Using the Login button

The main feature of the thiss-js software is the active login button which uses browser local store to remember and present the last Identity Provider selection made by the user. For most use-cases this completely elliminates the search/find/select UX for most interactions with your SP since most users rely on the same IdP for all their logins to a site. In order to take advantage of this feature you must do two things:

  1. Display the login button component somewhere on your SP login page
  2. Integrate the javascript API of the button component with your SAML SP software stack.

The first step is easy to describe in general but the second step depends on exactly how your SAML implementation works. We provide examples below for the Shibboleth SP but if you run something other than Shibboleth you need to consult your documentation to figure out how the integration works.

## Displaying the Login Button

Include the following HTML somewhere on your SPs login page:

```
<script src="https://use.thiss.io/thiss.js"/>
<div id="login"/>
<script>
window.onload = function() {
   thiss.DiscoveryComponent.render({
      loginInitiatorURL: 'https://sp.example.com/Shibboleth.sso/Login?target=https://sp.example.com/',
   }, '#login');
};
</script>
```

There are three parts to this:

 1. Include the thiss.js component. It is important that you retrieve the component from the same domain as the thiss-js service is provided from.
 2. Include a *div* with the id *login* - this can be anywhere in your markup where you want the button to appear and doesn't have to sit next to the script tags.
 3. Invoke the DiscoveryComponent.render function as a handler for the onload event on the window. This will cause the button to initialize as soon as the window has finished loading. It is possible to initialize the component earlier but this may cause it to behave unpredictably - YMWV.

## Integrating the Login Button with your SAML SP

The example above works out of the box for Shibboleth assuming you have configured https://use.thiss.io/ds as the discovery service as in the example above. The Shibboleth simplified SP configuration uses the url */Shibboleth.sso/Login* to trigger an authentication request using the discovery service configured in the *&lt;SSO&gt;* element.

In general the idea is to provide two hooks for the button component: 

 1. A way to initialize a SAML discovery protocol request in the SAML SP
 2. A way to receive the response from the SAML discovery protocol request

For Shibboleth the loginInitiatorURL serves both purposes but in general you need to provide two parameters *discoveryRequest* and *discoveryResponse* which can be either URLs (in which case a redirect is performed) or JavaScript functions that are called by the component. 

The *discoveryRequest* function is called with a single argument containing a JS object representing the chosen IdP - parameters include entity ID, icon, title etc. Normally this function will be used to initialize a SAML authentication request to the identity provider identified by *entity.entityID*.

For Shibboleth this is all handled by providing the single *loginInitiatorURL* parameter as in the example above.
