# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.

For changes to documentation only (no schema changes), start from step 4.

For changes to the theme only, start from step 7.

## 1. Pin extensions

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Each release of the standard should pin to specific versions of each [core extension](http://standard.open-contracting.org/latest/en/extensions/#core-extensions). Community extensions are not pinned. The steps are:

1. Review open pull requests and changes since last release of core extensions
1. Create new releases of core extensions
1. Create a new release of the extension registry to point to the new releases of extensions
1. Pull extensions' Markdown files into the standard
1. Set the documentation build process to use the new extension registry tag

### Review open pull requests and changes since last release of core extensions

For each *core* extension:

1. Open the extension's [homepage](https://github.com/open-contracting/ocds_lots_extension) on GitHub
1. Review [open pull requests](https://github.com/open-contracting/ocds_lots_extension/pulls) and discuss whether to merge any
1. Open the extension's [releases](https://github.com/open-contracting/ocds_lots_extension/releases) (under the repository title and description from the extension's homepage)
1. Click to view the [commits since the last release](https://github.com/open-contracting/ocds_lots_extension/compare/v1.1...master) (under the release's heading). If there are no new commits, skip the rest of this step.
1. Check the changes against the [changelog](http://standard.open-contracting.org/latest/en/schema/changelog/#changelog) for the version of OCDS being deployed
1. Before publishing the release, discuss any substantive changes, i.e. not simple typo or documentation updates, which aren't included in the changelog

### Create new releases of core extensions

For each *core* extension:

1. From the list of releases, click *Draft a new release*
1. In the *Tag version* field, enter the version of OCDS being deployed in *vmajor.minor.patch* format, e.g. `v1.1.1`
1. In the *Release title* field, enter a title, e.g. "Fixed version for OCDS 1.1.1"
1. Enter a brief summary of changes, e.g. "Typo fixes", and click *Publish release*

### Pull extensions' Markdown files into the standard

```bash
cd standard/docs/en/extensions
# edit get-readmes.py and set GIT_REF to e.g. `v1.1.1`
./get-readmes.py
```

### Set the documentation build process to use the new extension registry tag

Edit `standard/docs/en/conf.py` and set `extension_registry_git_ref` to e.g. `v1.1.1`.

## 2. Check schema IDs

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Check that the `id` property at the top of each JSON schema file have been updated to reflect the current *major__minor__patch* version number.

For example:

```json
{
  "id": "http://standard.open-contracting.org/schema/1__1__1/record-package-schema.json",
  "$schema": "http://json-schema.org/draft-04/schema#"
}
```

## 3. Make the validation schema

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

The _versioned-release-validation-schema.json_ file exists for validation of versioned releases. It is currently programatically generated from the latest version of the schema and committed to the repository.

To run this script:

1. Update `standard/schema/utils/make_validation_schema.py` to refer to the correct version number (line 94).
1. Run `standard/schema/utils/make_validation_schema.py`
1. commit the updated _versioned-release-validation-schema.json_ file to the repository.

## 4. Push and pull updated translations

1. Run `tx push -s` to push updated source files to Transifex.
1. Run `tx pull -a -f` to pull updated translation files to the repository.
1. Commit the updated translation files to the repository.

```eval_rst
  .. todo::
    How can we test translation and be sure all strings had valid translations?
```

## 5. Merge the dev branch

The dev working branch should be merged into the relevant live branch, e.g. merge `1.1-dev` onto `1.1`. Do this in the GitHub interface, or locally with a no-ff merge (so that we get a merge commit to record when the live branch was updated). If required, this may happen by first merging a patch dev branch into the dev branch for a major or minor version, and then merging onwards into the live branch.

## 6. Create a tagged release

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Create a tagged release named e.g. `1__1__0`

## 7. Build on Travis

Step 5 will trigger a build on Travis. For changes to the theme, hit rebuild on the previous build for the relevant live branch.

Travis copies the built docs to the dev server, you can check they look okay there. e.g. for 1.1:
[http://ocds-standard.dev3.default.opendataservices.uk0.bigv.io/1.1/en/](http://ocds-standard.dev3.default.opendataservices.uk0.bigv.io/1.1/en/)

## 8. Copy the files to the live server

(See the [servers](../../servers) page for more info on how our servers are set up.)

Each deploy has its own unique folder on the live server (including the date and a sequence number). The bare version number is then symlinked. This makes it easy to roll back the live docs.

Set some variables:

```bash
VER=1.1            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
```

Copy from dev server to your local box:

```bash
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/${VER} \
  ${VER}-${DATE}-${SEQ}
```

Copy from your local box to the live server:

```bash
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/
```

Symlink the version number:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/${VER}"
```

If a new language is supported, edit `http://standard.open-contracting.org/robots.txt`

## 9. Copy the schema into place

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Copy the JSON from the schema directory of the build to `/home/ocds-docs/web/schema/[release_tag]` on the live server, e.g. for 1.1.1:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io
mkdir /home/ocds-docs/web/schema/1__1__1/
cp -r /home/ocds-docs/web/1.1/en/*.json /home/ocds-docs/web/schema/1__1__1/
```

The JSON files are then visible at [http://standard.open-contracting.org/schema/1__1__1/](http://standard.open-contracting.org/schema/1__1__1/).

## 10. Update the "latest" branch

If the build should also appear at [/latest/](http://standard.open-contracting.org/latest/), then update the `latest` branch on GitHub to point to the same commit. Wait for the Travis build, then repeat step 8 with `VER=latest`.

Doing a build is necessary because some URLs are updated with the branch name (e.g. links in the schema).

## 11. Update the Apache config

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

For a new live version, you will need to edit:

* [live_versions in the Apache config](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L16)
* [version switcher](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/version-options.html)
* [dev](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_dev.html) and [old](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_old.html) banners

## 12. Update the OCDS validator

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

* Set up a development instance of CoVE using the new schema, and run tests against it
* Update the live CoVE deployment to use the new schema

## FAQ

### How can I find out what the standard looked like at 1.0

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

### How can I find out what the standard looked like at 1.1.0

TBC. (Is the answer to look for a tagged release?)
