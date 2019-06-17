---
layout: page
permalink: /gettingstarted/
title: Getting Started
---

In order to run your own instance of the thiss.io software you need two things:

1. An MDQ service that supports the search API
2. The [thiss-js](https://github.com/TheIdentitySelector/thiss-js) software

The [pyFF.io](https://pyff.io) implemenation of MDQ is known to work with thiss-js but other MDQ implemenations should also be made to work with some effort. The main issue is that the MDQ service nees to support search on the /entities/ endpoint by passing a query-parameter ('q') containing search terms. Exactly how seardch is implemented is up to the implmementation but the caller (thiss-js) expects application/json response as described in the README of [thiss-ds-js](https://github.com/TheIdentitySelector/thiss-ds-js).

Running an instance of thiss-js can be done by launching a docker container. A simple setup assuming a pyFF backend is described in the README of [thiss-js](https://github.com/TheIdentitySelector/thiss-ds-js).
