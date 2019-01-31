# Servers

[standard.open-contracting.org](http://standard.open-contracting.org) and [standard.open-contracting.org/review/](http://standard.open-contracting.org/review/) are hosted by Open Data Services on Bytemark VPS's. Contact [code@opendataservices.coop](mailto:code@opendataservices.coop) with any queries that relate directly to servers.

Deployments are carried out using Salt, with configuration in [opendataservices-deploy](https://github.com/OpenDataServices/opendataservices-deploy).

DNS and proxies:

* `live2.default.opendataservices.uk0.bigv.io`: [standard.open-contracting.org](http://standard.open-contracting.org/) points to this server. It is a reverse proxy in front of `dev3` and `cove-live-ocds`.

Hosting the documentation:

* `live2.default.opendataservices.uk0.bigv.io`: hosts the production version of the documentation of the core standard (e.g. [latest](http://standard.open-contracting.org/latest/), [1.0](http://standard.open-contracting.org/1.0/) and [1.1](http://standard.open-contracting.org/1.1/)) and its profiles (e.g. [Public Private Partnerships](http://standard.open-contracting.org/profiles/ppp/latest/en/)). It is shared with other standards.
* `dev3.default.opendataservices.uk0.bigv.io`: hosts the development versions of the documentation for the core standard and its profiles. Travis has SFTP access to push developments builds to this server. It is shared with other standards.
* GitHub Pages hosts the [Extension Explorer](https://extensions.open-contracting.org/).

Hosting the Data Review Tool:

* `cove-live-ocds`: hosts the [production version](http://standard.open-contracting.org/review/).
* `dev.cove.opendataservices.coop`: hosts a [development version](http://dev.cove.opendataservices.coop/review/). It is shared with other standards.

Hosting the CRM:

* `crm.open-contracting.org`: hosts the Redmine CRM, on a Linode VPS, managed by Dogsbody Technology. Contact [support@dogsbodytechnology.com](mailto:support@dogsbodytechnology.com).

Hosting Kingfisher:

* `ocdskingfisher-dev.default.opendataservices.uk0.bigv.io`

`dev.cove` also hosts subdomains.
