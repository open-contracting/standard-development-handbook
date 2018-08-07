# Deployment

A profile's deployment is simpler than the standard's [deployment](../../../standard/technical/deployment). If a profile is unversioned, some of the below may be irrelevant.

## Schemas and extensions

### 1. Review extensions

#### Review pull requests and recent changes

Follow the [standard's instructions](../../../standard/technical/deployment#review-pull-requests-and-recent-changes), substituting the profile's extensions for core extensions.

#### Create new releases of core extensions

The governance process will establish whether to create a new release of any core extensions within the profile. If appropriate, follow the [standard's instructions](../../../standard/technical/deployment#create-new-releases-of-core-extensions).

### 2. Perform periodic updates, if appropriate

*Nothing to do.*

### 3. Update version numbers, validation schema and changelog

Update `release` in `docs/conf.py` to e.g. `1.0.0`. Update `version` if appropriate.

Update the profile's changelog (if any) with a summary of the changes to the profile's extensions.

### 4. Integrate extensions

[Build the profile](../build#build-the-profile).

## Merge and release

Follow the [standard's instructions](../../../standard/technical/deployment#merge-and-release).

## Build and deploy

### 1. Build on Travis

Follow the [standard's instructions](../../../standard/technical/deployment#build-on-travis).

### 2. Copy the files to the live server

Follow the [standard's instructions](../../../standard/technical/deployment#copy-the-files-to-the-live-server), but change `BASEDIR` to `/home/ocds-docs/web/profiles/${PROFILE}/` where `PROFILE` is e.g. `ppp`.

### 3. Copy the schema into place

```eval_rst
  .. todo::
    Update this section once the steps are determined. `See GitHub issue <https://github.com/open-contracting/public-private-partnerships/issues/172>`_.
```

### 4. Update the "latest" branch

Follow the [standard's instructions](../../../standard/technical/deployment#update-the-latest-branch).


### 5. Update the deployment repository

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

```eval_rst
  .. todo::
    Should profiles with versions have an ``old`` banner?
```

* For major, minor or patch versions, edit the profile's version switcher e.g. for [OCDS for PPPs](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/version-options-profiles-ppp.html)
* For major and minor versions, edit `live_versions` in the Apache configuration file, e.g. for [OCDS for PPPs](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L17)
* For major and minor versions, edit the `dev` (e.g. [OCDS for PPPs](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_dev_profiles_ppp.html)) and `old` banners
