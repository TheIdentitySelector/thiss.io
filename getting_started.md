---
layout: page
permalink: /gettingstarted/
title: Getting Started
---

There are two ways to use thiss: Either point your SP to an existing service instance or run your own instance. Most SPs will want to use an existing service instance but some may need or want to run their own instance of thiss - for instance to have full control over the IdPs listed in the discovery service. 

# Using an existing service

In order to connect to an existing service instance typically means follow instructions similar to [the instructions for how to connect to the demo service](/use/).

# Running your own instance

Runing your own instance of thiss-js involves two things:

1. An MDQ service that supports the [search API extension](https://github.com/IdentityPython/pyFF/wiki/Extensions-to-MDQ)
2. The [thiss-js](https://github.com/TheIdentitySelector/thiss-js) software

The [pyFF.io](https://pyff.io) implemenation of MDQ is known to work with thiss-js but other MDQ implemenations should also be made to work with some effort. The main issue is that the MDQ service nees to support search on the /entities/ endpoint by passing a query-parameter ('q') containing search terms. Exactly how seardch is implemented is up to the implmementation but the caller (thiss-js) expects application/json response as described in the README of [thiss-ds-js](https://github.com/TheIdentitySelector/thiss-ds-js).

Running an instance of thiss-js can be done by launching a docker container. A simple setup assuming a pyFF backend is described in the README of [thiss-js](https://github.com/TheIdentitySelector/thiss-ds-js).
