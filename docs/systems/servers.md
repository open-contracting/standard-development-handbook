# Servers

[standard.open-contracting.org](http://standard.open-contracting.org) and [standard.open-contracting.org/review/](http://standard.open-contracting.org/review/) are hosted by Open Data Services on Bytemark VPS's. Contact [code@opendataservices.coop](mailto:code@opendataservices.coop) with any queries that relate directly to servers.

Deployments are carried out using Salt, with configuration in [opendataservices-deploy](https://github.com/OpenDataServices/opendataservices-deploy).

## DNS and proxies

* `live2.default.opendataservices.uk0.bigv.io`: [standard.open-contracting.org](http://standard.open-contracting.org/) points to this server. It is a reverse proxy in front of `dev3` and `cove-live-ocds`.

## Documentation

* `live2.default.opendataservices.uk0.bigv.io`: hosts the production version of the documentation of the core standard (e.g. [latest](http://standard.open-contracting.org/latest/), [1.0](http://standard.open-contracting.org/1.0/) and [1.1](http://standard.open-contracting.org/1.1/)) and its profiles (e.g. [Public Private Partnerships](http://standard.open-contracting.org/profiles/ppp/latest/en/)). It is shared with other standards.
* `dev3.default.opendataservices.uk0.bigv.io`: hosts the development versions of the documentation for the core standard and its profiles. Travis has SFTP access to push developments builds to this server. It is shared with other standards.
* GitHub Pages hosts the [Extension Explorer](https://extensions.open-contracting.org/).

The documentation servers use Apache to serve mostly static files, 
some redirects and some proxy passes to dynamic systems such as the [Data Review Tool](http://standard.open-contracting.org/review/).

The Apache config files are deployed by Salt and the sources can be seen at 

* [Live](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf)
* [Dev](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-dev.conf)

### Version and Language Switcher

The Version and Language switcher are both powered by Apache redirects. This way, the webpage simply has a select box and a form. 
The user goes to a `switcher` URL, and an Apache redirect redirects the user to the desired page.

To do this, it has to know what branches there are, and you can see salt variables that list the branches in the config files:

* `live_versions`
* `infrastructure_live_versions`

Search for `switcher` in the Apache conf files to see the config for this.

## Data Review Tool

* `cove-live-ocds`: hosts the [production version](http://standard.open-contracting.org/review/).
* `dev.cove.opendataservices.coop`: hosts a [development version](http://dev.cove.opendataservices.coop/review/). It is shared with other standards.

## CRM

* `crm.open-contracting.org`: hosts the Redmine CRM, on a Linode VPS, managed by Dogsbody Technology. Contact [support@dogsbodytechnology.com](mailto:support@dogsbodytechnology.com).

## Kingfisher

* `scrape.kingfisher.open-contracting.org`
* `archive.kingfisher.open-contracting.org`

`dev.cove` also hosts subdomains.
