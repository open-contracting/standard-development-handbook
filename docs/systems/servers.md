# Servers

[standard.open-contracting.org](http://standard.open-contracting.org) and [standard.open-contracting.org/validator/](http://standard.open-contracting.org/validator/) are hosted by Open Data Services on VPS's provided by Bytemark. Contact [code@opendataservices.coop](mailto:code@opendataservices.coop) with any queries that relate directly to servers.

DNS and proxies:

* `live2`: [standard.open-contracting.org](http://standard.open-contracting.org/) points to this server. It is a reverse proxy in front of `dev3` and `cove-live-ocds`.

Hosting the documentation:

* `live2`: hosts the production version of the documentation of the core standard (e.g. [latest](http://standard.open-contracting.org/latest/), [1.0](http://standard.open-contracting.org/1.0/) and [1.1](http://standard.open-contracting.org/1.1/)) and its profiles (e.g. [Public Private Partnerships](http://standard.open-contracting.org/profiles/ppp/latest/en/)).
* `dev3`: hosts the development versions of the documentation for the core standard and its profiles. Travis has SFTP access to push developments builds to this server.

Hosting the validator:

* `cove-live-ocds`: hosts the [production version]((http://standard.open-contracting.org/validator/)) of the validator.
* `cove-dev`: hosts a [development version](http://dev.cove.opendataservices.coop/validator/) of the validator.

`cove-dev` also hosts subdomains.
