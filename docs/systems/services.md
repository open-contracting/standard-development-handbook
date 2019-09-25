# Services

The staff of the following organizations may have administrative roles:

* [Open Contracting Partnership](https://www.open-contracting.org/about/team/) (OCP)
* [Open Data Services Co-operative](http://opendataservices.coop) (ODS)
* [Iniciativa Latinoamericana por los Datos Abiertos](https://idatosabiertos.org/acerca-de-nosotros/) (ILDA)

## Google

### Analytics

There should be at most two [users](https://analytics.google.com/analytics/web/#/a35677147w162037252p163071392/admin/suiteusermanagement/account) with all permissions from OCP. There should be at most two users with the Read & Analyze permissions from each other organization.

### Cloud Platform

[IAM](https://console.cloud.google.com/iam-admin/iam?organizationId=1015889055088&project=ocds-172716) should only include Google-managed service accounts, `ods-crm-redmine-backup` and `data@open-contracting.org`. [Service accounts](https://console.cloud.google.com/iam-admin/serviceaccounts?organizationId=1015889055088&project=ocds-172716) should only include default service accounts and `ods-crm-redmine-backup`. There should be only one project ([`ocds`](https://console.cloud.google.com/home/dashboard?folder=&project=ocds-172716)), and it should only use two storage buckets (`crm-open-contracting-org-daily-backups` and `crm-open-contracting-org-weekly-backups`).

### Groups

* [standard-discuss](https://groups.google.com/a/open-contracting.org/forum/#!forum/standard-discuss)

There should be at most two members with the [Owner](https://support.google.com/a/answer/167094?hl=en) role from OCP. There should be at most two members with the Manager role from each other organization.

### Webmaster Central

There should be at most two [verified owners](https://www.google.com/webmasters/verification/details?hl=en&siteUrl=https://www.open-contracting.org/) from each organization.

## ReadTheDocs

There should be at most two [users](https://readthedocs.org/dashboard/ocds-standard-development-handbook/users/) with the Maintainer role from each of OCP and ODS, excluding organization-wide accounts.

## Redash

There should be at most two users in the [admin](http://live.redash.opencontracting.uk0.bigv.io:9090/groups/1) group from each of OCP and ODS, excluding organization-wide accounts.

## Redmine

There should be at most two [users](https://crm.open-contracting.org/users) with the Administrator role from each of OCP and ODS, excluding organization-wide accounts.

## Transifex

Transifex is used by ODS for multiple clients. There should be at most two members with the [Project Maintainer and Team Manager](https://docs.transifex.com/teams/understanding-user-roles) roles from OCP.
