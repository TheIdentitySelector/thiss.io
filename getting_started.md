---
layout: page
permalink: /gettingstarted/
title: Getting Started
---

The Coalition for Seamless Access provides the thiss service to enable several different “flavors” of implementation:

* **Limited** - lets you use the Seamless Access discovery service for users to find and sign into their preferred Identity Provider, but doesn’t integrate this service into your site.
* **Standard** - lets you use the Seamless Access service to display the button on your site, and use the Seamless Access discovery and persistence services as integrated components on your site.
* **Advanced** - provides you with the Seamless Access persistence service while giving you greater control over the appearance of the service on your site, and what Identity Providers (IdPs) you include in your discovery service.

# Using the Seamless Access Service or thiss Software

To implement the Seamless Access **Limited** or **Standard** 'flavors', you will be using the Seamless Access service which is a hosted instance of the thiss software. This service provides the core benefits of Seamless Access with minimal work. Most Service Providers (SPs) will prefer this option.

To implement the **Advanced** features, you will need to use the thiss software to run your own instance of the service.

# Getting Started - "Limited" Flavor

For the "Limited" flavor, you will implement:

* Discovery Service Integration - _Integrate the Seamless Access service to use it as your Discovery Service._

See the [Integration Guide](/integration/) to learn how to configure your Service Provider (SP) software stack.

# Getting Started - "Standard" Flavor

For the "Standard" flavor, you will implement:

* Discovery Service Integration - _Integrate the Seamless Access service to use it as your Discovery Service._
* Display of Seamless Access Login Button - _Use the Seamless Access service to display the login button component on your SP login page._
* Integration of Login Button with your SAML SP - _Integrate the Seamless Access service to use it as your Discovery Service._

See the [Integration Guide](/integration/) for details on how to implement.

# Getting Started - "Advanced" Flavor

The Advanced option provides significant control the display and behavior of the software and service, though requires you to run the software yourself. Running your own instance of thiss-js involves two things:

1. An MDQ service that supports the [search API extension](https://github.com/IdentityPython/pyFF/wiki/Extensions-to-MDQ)
2. The [thiss-js](https://github.com/TheIdentitySelector/thiss-js) software

The [pyFF.io](https://pyff.io) implementation of MDQ is known to work with thiss-js but other MDQ implementations should also be made to work with some effort. The main issue is that the MDQ service needs to support search on the /entities/ endpoint by passing a query-parameter ('q') containing search terms. Exactly how search is implemented is up to the implementation but the caller (thiss-js) expects application/json response as described in the README of [thiss-ds-js](https://github.com/TheIdentitySelector/thiss-ds-js).

Running an instance of thiss-js can be done by launching a docker container. A simple setup assuming a pyFF backend is described in the README of [thiss-js](https://github.com/TheIdentitySelector/thiss-ds-js).

While some details for implementation of the "Advanced" flavor can be found in the [Integration Guide](/integration/), more detailed documentation can be found in the [Discovery Service Client API Repository README](https://github.com/TheIdentitySelector/thiss-ds-js/blob/master/README.md).

# An Example Implementation

You can see an example of the "Standard" implementation at our [Demo Service](https://service.seamlessaccess.org/). This site provides an example of the standard behavior, and can provide insight for your implementation.

