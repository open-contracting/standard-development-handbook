# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.

For changes to documentation only (no schema changes), start from step 4.

For changes to the theme only, start from step 7.

## 1. Freeze extensions

Each release of the standard should pin to specific versions of each extension in [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions). Community extensions are not pinned.

This is currently achieved by:

* Creating a tagged release of each extension
* Creating a tagged release of the extension registry that points to these specific versions
* Pulling extensions' Markdown files
* Setting the documentation build process to refer to the relevant extension registry tag

### Pinning extensions: worked example

For each **core extension**:

#### Review outstanding pull requests and changes since last release

1. Open the relevant repository in the GitHub web interface ([example](https://github.com/open-contracting/ocds_lots_extension))
1. Review any outstanding [pull requests](https://github.com/open-contracting/ocds_lots_extension/pulls) and discuss these to determine whether they should be merged before pinning the extension
1. Under the repository title and description, click **Releases** to view the list of existing releases ([example](https://github.com/open-contracting/ocds_lots_extension/releases))
1. Under the title of the most recent release, the number of commits since that release will be listed, if there are no commits since the last release then skip to 'Publish a new release', otherwise click the link to view the list of changes since the last release ([example](https://github.com/open-contracting/ocds_lots_extension/compare/v1.1...master))
1. Check the list of changes since the last release against the [changelog](http://standard.open-contracting.org/latest/en/schema/changelog/#changelog) for the version of OCDS being deployed
1. Before publishing the release, discuss any substantive changes, i.e. not simple typo or documentation updates, which aren't included in the changelog

#### Publish a new release

1. From the list of releases, click **Draft a new release**
1. In the 'Tag version' field, enter the version of OCDS being deployed in _vmajor.minor.patch_ format, e.g. `v1.1.1`
1. In the 'Release title' field, enter a title, e.g. 'Fixed version for OCDS 1.1.1'
1. Enter a brief summary of changes, e.g. 'Typo fixes', and click **Publish release**

### Pulling extension documentation

```bash
cd standard/docs/en/extensions
# edit get-readmes.py and set GIT_REF to e.g. `v1.1.1`
./get-readmes.py
```

### Setting documentation build extension registry tag

Edit `standard/docs/en/conf.py` and set `extension_registry_git_ref` to e.g. `v1.1.1`.

## 2. Check schema IDs

Check that the `id` property at the top of each JSON schema file have been updated to reflect the current major__minor__patch version number.

For example:

```json
{
  "id": "http://standard.open-contracting.org/schema/1__1__1/record-package-schema.json",
  "$schema": "http://json-schema.org/draft-04/schema#"
}
```

## 3. Make validation schema

The _versioned-release-validation-schema.json_ file exists for validation of versioned releases. It is currently programatically generated from the latest version of the schema and committed to the repository.

To run this script:

1. Update `standard/schema/make_validation_schema.py` to refer to the correct version number (Line 94)
1. Run `make_validation_schema.py`

Then commit the updated _versioned-release-validation-schema.json_ file to the repository.

## 4. Push and pull updated translations

Run `tx push -s` to push updated sources files to Transifex.

Run `tx pull -a -f` to pull all updated translation files down locally.

Commit the updated translations to the repository.

```eval_rst
  .. todo::
    How can we test translation and be sure all strings had valid translations?
```

## 5. Merge the dev branch

The dev working branch should be merged into the relevant live branch, e.g. merge `1.1-dev` onto `1.1`. Do this in the GitHub interface, or locally with a no-ff merge (so that we get a merge commit to record when the live branch was updated). If required, this may happen by first merging a patch dev branch into the dev branch for a major or minor version, and then merging onwards into the live branch.

## 6. Create a tagged release

(Major/Minor/Patch versions only) Create a tagged release named e.g. `1__1__0`

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

(Major/Minor/Patch versions only) Copy the JSON from the schema directory of the build to `/home/ocds-docs/web/schema/[release_tag]` on the live server, e.g. for 1.1.1:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io
mkdir /home/ocds-docs/web/schema/1__1__1/
cp -r /home/ocds-docs/web/1.1/en/*.json /home/ocds-docs/web/schema/1__1__1/
```

The JSON files are then visible at [http://standard.open-contracting.org/schema/1__1__1/](http://standard.open-contracting.org/schema/1__1__1/).

## 10. Update the "latest" branch

If the build should also appear at [/latest/](http://standard.open-contracting.org/latest/), then update the `latest` branch on GitHub to point to the same commit. Wait for the travis build, then repeat step 8 with `VER=latest`.

Doing a build is necessary because some URLs are updated with the branch name (e.g. links in the schema).

## 11. Update the Apache config

(Major/Minor versions only) For a new live version, you will need to edit:

* [live_versions in the Apache config](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L16)
* [version switcher](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/version-options.html)
* [dev](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_dev.html) and [old](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_old.html) banners

## 12. Update the OCDS validator

(Major/Minor versions only)

* Set up a development instance of CoVE using the new schema, and run tests against it
* Update the live CoVE deployment to use the new schema

## FAQ

### How can I find out what the standard looked like at 1.0?

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

### How can I find out what the standard looked like at 1.1.0?

TBC. (Is the answer to look for a tagged release?)
