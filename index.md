---
layout: home
---

![Coalition for Seamless Access Logo](/assets/img/RA21-New-Blue.png)

The Identity Selector Software (thiss.io) is an implementation of an identity selector supported by [the Coalition for Seamless Access](https://seamlessaccess.org/). It implements a discovery service using the [RA21.org](https://ra21.org) [recommended practices for discovery UX](https://groups.niso.org/apps/group_public/download.php/21376/NISO_RP-27-2019_RA21_Identity_Discovery_and_Persistence-public_comment.pdf).

Discovery services are used to facilitate user single sign in for [Federated Identity Management](https://en.wikipedia.org/wiki/Federated_identity). This implementation supports the SAML metadata discovery protocol, and is optimized for the global set of research and education access federations, for example, user sign in to services via their university or institutional login credentials. 

If you have reached here looking for a discovery service for your relying party you most likely want to head over to [seamlessaccess.org](https://seamlessaccess.org). If you are a developer or integrator or a federation operator who really really really fancy running your own stuff or have advanced integration needs ... read on!

Source code can be found on GitHub: [TheIdentitySelector](https://github.com/TheIdentitySelector/). Important repositories include the following:

* [thiss-js](https://github.com/TheIdentitySelector/thiss-js): The discovery service including a Dockerfile for running as a standalone service. Built using thiss-ds-js and thiss-jquery-plugin.
* [thiss-ds-js](https://github.com/TheIdentitySelector/thiss-ds-js): A set of clients for the discovery service. Can be used to implement a DS connected to a central persistence service. This is the low-level API to a thiss-js instance.
* [thiss-jquery-plugin](https://github.com/TheIdentitySelector/thiss-jquery-plugin): A jQuery plugin for building search-based identity selectors. If you are a federation operator looking to build your own integrated discovery service you might want to look at this.
* [this-mdq](https://github.com/TheIdentitySelector/thiss-mdq): An implementation of the metadata query protocol (MDQ) for JSON metadata only. Only go here if you are running a standalone instance of thiss-js and [pyFF.io](https://pyff.io) or similar isn't fast enough.
