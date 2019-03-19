# Infrastructure

## Deployment

This process is the [same as the process for the Open Contracting Data Standard](../../standard/technical/deployment.md), with some changes, which are listed here.


### 2. Copy the files to the live server

* set `BASEDIR` to `/home/ocds-docs/web/infrastructure`


### 3. Copy the schema into place

* Copy the JSON from the schema directory of the build to `/home/ocds-docs/web/infrastructure/schema/[release_tag]` on the live server, e.g. for 0.9.0:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io
mkdir /home/ocds-docs/web/infrastructure/schema/0__9__0/
cp -r /home/ocds-docs/web/infrastructure/0.9/en/*.json /home/ocds-docs/web/infrastructure/schema/0__9__0/
```
### 5. Update the deployment repository

* [For major and minor versions, edit `infrastructure_live_versions` in the Apache configuration file](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L18)

