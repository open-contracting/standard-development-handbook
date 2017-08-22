# GitHub Integrations

## Travis CI

Used to run tests, and also build the OCDS Standard and OCDS Profiles documentation.

### Travis cron

Travis cron is currently used for the [extension_tester](https://github.com/open-contracting/extension_tester). The cron run is the same as a normal run of the tests (defined in `.travis.yml`). Cron can be enabled/disable on the [travis settings page for the repo](https://travis-ci.org/open-contracting/extension_tester/settings). Notifications currently come to code [at] opendataservices [dot] coop.

## ReadTheDocs

Used only to build these docs, see [the README](https://github.com/open-contracting/standard-development-handbook/blob/master/README.md).

## Requires.io

Emails code [at] opendataservices [dot] coop when a requirement we're using has a security vulnerability.

The web interface can also we used to see what requirements are out of date:
* [standard](https://requires.io/github/open-contracting/standard/requirements/)
* [sample-data](https://requires.io/github/open-contracting/sample-data/requirements/)
