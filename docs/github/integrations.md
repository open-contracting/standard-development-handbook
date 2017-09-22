# Integrations

## Travis CI

Used to run tests, and also build the documentation of the core standard and its profiles.

### Travis cron jobs

[Travis cron jobs](https://docs.travis-ci.com/user/cron-jobs/) is used by [extension_tester](https://github.com/open-contracting/extension_tester). A job run is the same as a normal run of the tests defined in `.travis.yml`. The job can be enabled or disabled via the [Travis settings for the repository](https://travis-ci.org/open-contracting/extension_tester/settings). Notifications go to code@opendataservices.coop, as [configured in `.travis.yml`](https://docs.travis-ci.com/user/notifications/#Configuring-email-notifications).

## ReadTheDocs

Used only to build the handbook. See [the readme](https://github.com/open-contracting/standard-development-handbook/blob/master/README.md).

## Requires.io

Emails code@opendataservices.coop when a requirement has a security vulnerability, as configured on the [requires.io hooks page](https://requires.io/github/open-contracting/hooks/). The web interface can also we used to see what requirements are out of date:

* [standard](https://requires.io/github/open-contracting/standard/requirements/)
* [sample-data](https://requires.io/github/open-contracting/sample-data/requirements/)
