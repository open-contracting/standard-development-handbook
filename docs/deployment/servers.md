# Servers

The OCDS standard website, and the OCDS validator are hosted by Open Data
Services on VPS's provided by bytemark. Contact code [at] opendataservices
[dot] coop with any queries that relate directly to servers.

Hosting the standard:

* `live2` - [standard.open-contracting.org](http://standard.open-contracting.org/) points at this server. It acts as a reverse proxy in front of `dev3` and `cove-live-ocds`, and also hosts the live docs ie. [latest](http://standard.open-contracting.org/latest/), [1.0](http://standard.open-contracting.org/1.0/), [1.1](http://standard.open-contracting.org/1.1/) and live copies of profiles e.g. [http://standard.open-contracting.org/profiles/ppp/latest/en/](http://standard.open-contracting.org/profiles/ppp/latest/en/)
* `dev3` - hosts dev copies of the standard docs, and dev copies of profiles. Travis has sftp access to push dev builds directly to this server.

Hosting the validator:

* `cove-live-ocds` - live server hosts [http://standard.open-contracting.org/validator/](http://standard.open-contracting.org/validator/) behind the `live2` reverse proxy
* `cove-dev` - hosts [http://dev.cove.opendataservices.coop/validator/](http://dev.cove.opendataservices.coop/validator/) and subdomains
