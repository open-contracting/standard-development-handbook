# Servers

[standard.open-contracting.org](https://standard.open-contracting.org) and [standard.open-contracting.org/review/](https://standard.open-contracting.org/review/) are hosted by Open Data Services on Bytemark VPS's. Contact [code@opendataservices.coop](mailto:code@opendataservices.coop) with any queries that relate directly to servers.

Deployments are carried out using Salt, with configuration in [opendataservices-deploy](https://github.com/OpenDataServices/opendataservices-deploy).

## DNS and proxies

* `live.docs.opencontracting.uk0.bigv.io`: [standard.open-contracting.org](https://standard.open-contracting.org/) points to this server. It serves some static files, and is also a reverse proxy in front of `staging.docs.opencontracting.uk0.bigv.io` and `live.cove.opencontracting.uk0.bigv.io`.

## Documentation

* `live.docs.opencontracting.uk0.bigv.io`: hosts the production version of the documentation of the core standard (e.g. [latest](https://standard.open-contracting.org/latest/), [1.0](https://standard.open-contracting.org/1.0/) and [1.1](https://standard.open-contracting.org/1.1/)) and its profiles (e.g. [Public Private Partnerships](https://standard.open-contracting.org/profiles/ppp/latest/en/)).
* `staging.docs.opencontracting.uk0.bigv.io`: hosts the staging versions of the documentation for the core standard and its profiles. Travis has SFTP access to push developments builds to this server.
* GitHub Pages hosts the [Extension Explorer](https://extensions.open-contracting.org/).

### Apache

Apache serves static files, redirects and proxies requests to dynamic systems like the [Data Review Tool](https://standard.open-contracting.org/review/). The Apache config files, deployed by Salt, are:

* [live](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf)
* [live (include)](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf.include)
* [staging](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-staging.conf)
* [staging (include)](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-staging.conf.include)

The websites are browsable at:

* [live](https://standard.open-contracting.org/latest/en/)
* [staging](http://staging.standard.open-contracting.org/latest/en/)

There are also testing versions of both websites available. These are hosted on the same servers, but in different Apache virtual hosts. These can be used for testing changes to Apache redirects and proxy settings, before making those changes live. You can see an `if testing` check that can be used in the Apache configurations that Salt will render. The websites are browsable at:

* [live testing](http://testing.live.standard.open-contracting.org/latest/en/)
* [staging testing](http://testing.staging.standard.open-contracting.org/latest/en/)

### Version and Language Switchers

The version switcher links to a `/switcher` URL path with `branch` URL parameter. The language switcher links to a `/{version}/switcher` URL path with a `lang` URL parameter.

These are then redirected by Apache (search for `switcher` in the config files). To do so, Apache needs to know which branches exist, which are indicated using the Salt variables `live_versions` and `infrastructure_live_versions`.

### Redirects to extension website

With the release of 1.1.4, extensions are moved to a new website.

Old pages are redirected by Apache (search for `extensions.open-contracting.org` in the config files). To do so, Apache needs to know which languages are used, which are indicated using the Salt variables `langs` and `langs_ppp`.

### Standard Search

[Standard Search](https://github.com/OpenDataServices/standard-search) runs on `standard-search.open-contracting.org`. The [`search.js` file](https://github.com/open-contracting/standard_theme/blob/open_contracting/standard_theme/static/js/search.js) in the `standard_theme` repository sends a request to its search endpoint to retrieve search results.

The Travis deploy scripts send requests to its indexing endpoint to index the contents of: ([OCDS documentation](https://github.com/open-contracting/deploy/blob/master/deploy-standard.sh), [OCDS profiles](https://github.com/open-contracting/deploy/blob/master/deploy-profile.sh), and [OC4IDS documentation](https://github.com/open-contracting/deploy/blob/master/deploy-infrastructure.sh)).

## Data Review Tool

* `live.cove.opencontracting.uk0.bigv.io`: hosts the [production version](https://standard.open-contracting.org/review/).
* `dev.cove.opendataservices.coop`: hosts a [development version](http://dev.cove.opendataservices.coop/review/). It is shared with other standards.

## CRM

* `crm.open-contracting.org`: hosts the Redmine CRM, on a Linode VPS, managed by Dogsbody Technology. Contact [support@dogsbody.com](mailto:support@dogsbody.com).

## Kingfisher

OCDS Kingfisher is the data access and analysis platform for OCDS data. 

There is a hosted version of the software, called [Hosted Kingfisher](https://ocdskingfisher.readthedocs.io/en/latest/). 

### Hosting

There are two physical servers for Kingfisher, which have four roles - scrape, process, analyse and archive. 

* `scrape.kingfisher.open-contracting.org` hosts scrape, process and analyse
* `archive.kingfisher.open-contracting.org` hosts archive. 

These allocations may change, so always use the hostname to access services:
* `scrape.kingfisher.open-contracting.org`
* `process.kingfisher.open-contracting.org`
* `analyse.kingfisher.open-contracting.org`
* `archive.kingfisher.open-contracting.org`
