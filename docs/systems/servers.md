# Servers

[standard.open-contracting.org](http://standard.open-contracting.org) and [standard.open-contracting.org/review/](http://standard.open-contracting.org/review/) are hosted by Open Data Services on Bytemark VPS's. Contact [code@opendataservices.coop](mailto:code@opendataservices.coop) with any queries that relate directly to servers.

Deployments are carried out using Salt, with configuration in [opendataservices-deploy](https://github.com/OpenDataServices/opendataservices-deploy).

## DNS and proxies

* `live.docs.opencontracting.uk0.bigv.io`: [standard.open-contracting.org](http://standard.open-contracting.org/) points to this server. It serves some static files, and is also a reverse proxy in front of `staging.docs.opencontracting.uk0.bigv.io` and `cove-live-ocds-2.default.opendataservices.uk0.bigv.io`.

## Documentation

* `live.docs.opencontracting.uk0.bigv.io`: hosts the production version of the documentation of the core standard (e.g. [latest](http://standard.open-contracting.org/latest/), [1.0](http://standard.open-contracting.org/1.0/) and [1.1](http://standard.open-contracting.org/1.1/)) and its profiles (e.g. [Public Private Partnerships](http://standard.open-contracting.org/profiles/ppp/latest/en/)).
* `staging.docs.opencontracting.uk0.bigv.io`: hosts the staging versions of the documentation for the core standard and its profiles. Travis has SFTP access to push developments builds to this server.
* GitHub Pages hosts the [Extension Explorer](https://extensions.open-contracting.org/).

### Apache

Apache serves static files, redirects and proxies requests to dynamic systems like the [Data Review Tool](http://standard.open-contracting.org/review/). The Apache config files, deployed by Salt, are:

* [live](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf)
* [live (include)](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf.include)
* [staging](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-staging.conf)
* [staging (include)](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-staging.conf.include)

The websites are browsable at:

* [live](http://standard.open-contracting.org/latest/en/)
* [staging](http://staging.standard.open-contracting.org/latest/en/)

There are also testing versions of both websites available. These are hosted on the same servers, but in a different apache virtual host. These can be used for testing Apache redirects and proxy changes before making those changes live. You can see a `if testing` check that can be used in the apache configurations that salt will render. The websites are browsable at:

* [live testing](http://testing.live.standard.open-contracting.org/latest/en/)
* [staging testing](http://testing.staging.standard.open-contracting.org/latest/en/)

### Version and Language Switchers

The version switcher links to a `/switcher` URL path with `branch` URL parameter. The language switcher links to a `/{version}/switcher` URL path with a `lang` URL parameter.

These are then redirected by Apache (search for `switcher` in the config files). To do so, Apache needs to know which branches exist, which are indicated using the Salt variables `live_versions` and `infrastructure_live_versions`.

### Redirects to extension website

With the release of 1.1.4, extensions are moved to a new website.

Old pages are redirected by Apache (search for `extensions.open-contracting.org` in the config files). To do so, Apache needs to know which languages are used, which are indicated using the Salt variables `langs` and `langs_ppp`.

## Data Review Tool

* `cove-live-ocds`: hosts the [production version](http://standard.open-contracting.org/review/).
* `dev.cove.opendataservices.coop`: hosts a [development version](http://dev.cove.opendataservices.coop/review/). It is shared with other standards.

## CRM

* `crm.open-contracting.org`: hosts the Redmine CRM, on a Linode VPS, managed by Dogsbody Technology. Contact [support@dogsbody.com](mailto:support@dogsbody.com).

## Kingfisher

* `scrape.kingfisher.open-contracting.org`
* `archive.kingfisher.open-contracting.org`

`dev.cove` also hosts subdomains.
