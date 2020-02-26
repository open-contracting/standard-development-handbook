# Services

The staff of the following organizations may have administrative roles:

* [Open Contracting Partnership](https://www.open-contracting.org/about/team/) (OCP)
* [Open Data Services Co-operative](http://opendataservices.coop) (ODS)
* [Centro de Desarrollo Sostenible](http://www.cds.com.py) (CDS)

## Self-hosted

### SSH keys

The files referenced by `ssh_auth.present` in the [deploy](https://github.com/open-contracting/deploy) repository give users access to servers. All users should belong to the above organizations.

### Redash

There should be at most two users in the [admin](http://live.redash.opencontracting.uk0.bigv.io:9090/groups/1) group from each of OCP and ODS, excluding organization-wide accounts.

### Redmine

There should be at most two [users](https://crm.open-contracting.org/users) with the Administrator role from each of OCP and ODS, excluding organization-wide accounts.

## Third-party

### Airtable

There should be at most two [Owners](https://airtable.com/wspXFnEMMAgLMWfe0/workspace/billing). All users should belong to the above organizations.

### Amazon Web Services

See [Identity and Access Management](https://console.aws.amazon.com/iam/home?region=us-east-1#/home) for a list of users and permissions. We use S3 (Simple Storage Service) and SES (Simple Email Service).

### GitHub

The staff of the above organizations may be [members](https://github.com/orgs/open-contracting/people) of the [open-contracting](https://github.com/open-contracting) GitHub organization.

There should be at most two members with the [Owner](https://help.github.com/articles/permission-levels-for-an-organization/) role from each organization.

GitHub's [outside collaborators](https://help.github.com/articles/adding-outside-collaborators-to-repositories-in-your-organization/) feature should be used for all other users.

### Google

#### Admin

There should be a minimum of [Super Admin](https://admin.google.com/open-contracting.org/AdminHome?hl=en#DomainSettings/notab=1&role=9170516996784129&subtab=roles) users from OCP, and no other assigned admins.

*Less secure apps* is set to "Allow users to manage their access to less secure apps" for the open-contracting.org domain, and [*Allow less secure apps*](https://myaccount.google.com/lesssecureapps) is set to "ON" for the data@open-contracting.org user, so that Redmine can fetch mail.

#### Analytics

There should be at most two [users](https://analytics.google.com/analytics/web/#/a35677147w162037252p163071392/admin/suiteusermanagement/account) with all permissions from OCP. There should be at most two users with the Read & Analyze permissions from each other organization.

#### Cloud Platform

For the `ocds` project, [IAM](https://console.cloud.google.com/iam-admin/iam?organizationId=1015889055088&project=ocds-172716) should only include Google-managed service accounts, `ods-crm-redmine-backup` and `sysadmin@dogsbody.com`. [Service accounts](https://console.cloud.google.com/iam-admin/serviceaccounts?organizationId=1015889055088&project=ocds-172716) should only include default service accounts and `ods-crm-redmine-backup`. It should only use two storage buckets (`crm-open-contracting-org-daily-backups` and `crm-open-contracting-org-weekly-backups`). `sysadmin@dogsbody.com` must have the ["Storage Admin" role](https://cloud.google.com/storage/docs/access-control/iam-roles) (`roles/storage.admin`), to get the `storage.buckets.list` permission.

The other projects are `library` (two storage buckets), `glossary` (no resources) and `standard-maintenance-scripts` (no resources).

In case a new user needs to be given admin access to the `ocds` project, you can run, for example:

    gcloud projects add-iam-policy-binding ocds-172716 --member user:jmckinney@open-contracting.org --role roles/owner

#### Drive

All users with access to [this folder](https://drive.google.com/drive/folders/0B79uNIOfT24eZTZqZjNNblVrek0) should belong to the above organizations.

#### Groups

* [standard-discuss](https://groups.google.com/a/open-contracting.org/forum/#!forum/standard-discuss)

There should be at most two members with the [Owner](https://support.google.com/a/answer/167094?hl=en) role from OCP. There should be at most two members with the Manager role from each other organization.

#### Webmaster Central

There should be at most two [verified owners](https://www.google.com/webmasters/verification/details?hl=en&siteUrl=https://www.open-contracting.org/) from each organization.

### PyPi

* [json-merge-patch](https://pypi.org/manage/project/json-merge-patch/collaboration/)
* [libcoveoc4ids](https://pypi.org/manage/project/libcoveoc4ids/collaboration/)
* [libcoveocds](https://pypi.org/manage/project/libcoveocds/collaboration/)
* [ocds-babel](https://pypi.org/manage/project/ocds-babel/collaboration/)
* [ocdsextensionregistry](https://pypi.org/manage/project/ocdsextensionregistry/collaboration/)
* [ocdskit](https://pypi.org/manage/project/ocdskit/collaboration/)
* [ocdsmerge](https://pypi.org/manage/project/ocdsmerge/collaboration/)

There should be at most one user with the [Owner role](https://pypi.org/help/#collaborator-roles) from each of OCP and ODS (OpenDataServices). Only users who are reasonably expected to upload releases should have the Maintainer role. Depending on the package, these include:

* benwebb (Ben Webb)
* kindly (David Raznick)
* odscjames (James Baster)
* rhiaro (Amy Guy)

### ReadTheDocs

There should be at most two [users](https://readthedocs.org/dashboard/ocds-standard-development-handbook/users/) with the Maintainer role from each of OCP and ODS, excluding organization-wide accounts.

### Sentry

Sentry is used by ODS for multiple clients. There should be at least one member with the Member role from OCP on relevant projects.

### Transifex

Transifex is used by ODS for multiple clients. There should be at most two members with the [Project Maintainer and Team Manager](https://docs.transifex.com/teams/understanding-user-roles) roles from OCP.

### Trello

Trello is used by ODS for multiple clients. There should be at least one member from OCP on relevant boards.
