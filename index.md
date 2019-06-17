---
layout: home
---

About thiss.io
===

The Identity Selector Software (thiss.io) is an implementation of an identity selector (aka discovery
service). Currently the implementation supports the SAML metadata discovery protocol aswell as the 
[RA21.org](https://ra21.org) [recommended practices for discovery UX](https://groups.niso.org/apps/group_public/download.php/21376/NISO_RP-27-2019_RA21_Identity_Discovery_and_Persistence-public_comment.pdf).

Source code can be found on GitHub:
[TheIdentitySelector](https://github.com/TheIdentitySelector/)

Important repositories include the following:

* [thiss-js](https://github.com/TheIdentitySelector/thiss-js): The discovery service including a Dockerfile for easy deploy.
* [thiss-ds-js](https://github.com/TheIdentitySelector/thiss-ds-js): A set of clients for the discovery service. Can be used to implement a DS connected to a central persistence service.
* [this-mdq](https://github.com/TheIdentitySelector/thiss-mdq): An implementation of the metadata query protocol (MDQ) for JSON metadata only. 

