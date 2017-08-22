# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.

For changes just to documentation (no schema changes), start from step 4.

For theme changes, start from step 8.


## 1. Freeze extensions

Each release of the standard should pin to specific versions of each extension in [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions). Community extensions are not pinned. 

This is currently achieved by:

* Creating a tagged release of each extension
* Creating a tagged release of the extension registry that points to these specific versions
* Setting the documentation build process to refer to the relevant extension registry tag

### Pinning extensions: worked example

For each **core extension**:

#### Review outstanding pull requests and changes since last release

1. Open the relevant repository in the Github web interface ([example](https://github.com/open-contracting/ocds_lots_extension))
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

1. Update _standard/schema/make_validation_schema.py_ to refer to the correct version number (Line 94)
2. Run make_validation_schema.py

Then commit the updated _versioned-release-validation-schema.json_ file to the repository. 

## 4. Push and pull updated translations

Run `tx push -s` to push updated sources files to Transifex

Run `tx pull -a -f` to pull all updated translation files down locally.

Commit the updated translations to the repository. 

**ToDo**: How can we test translation and be sure all strings had valid translations? 

## 5. Merge standard

The dev working branch should be merged into the relevant live branch. 

e.g. merge 1.1-dev onto 1.1

Do this in the GitHub interface, or locally with a no-ff merge (so that we get a merge commit to record when the live branch was updated).

(If required, this may happen by first merging a patch dev branch into the dev branch for a major or minor version, and then merging onwards into the live branch)

## 6. Create a tagged release

Named e.g. 1__1__0

## 7. Copy the schema into place

If you've made a semantic update to the schema, that should be tagged with a
patch version (e.g. 1__0__1 on GitHub), and the json should be copied to
/home/ocds-docs/web/schema on live2.

e.g. for 1.1.1 there should be JSON files at [http://standard.open-contracting.org/schema/1__1__1/](http://standard.open-contracting.org/schema/1__1__1/).


## 8. Build on travis

Step 5. will trigger a build on travis. For changes to the theme, hit rebuild on the previous build for the relevant live branch.

Once this is done, check the staging site, e.g. for 1.1:
http://ocds-standard.dev3.default.opendataservices.uk0.bigv.io/1.1/en/

## 9. Copy the files:

```bash
VER=1.1            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
```

Copy from dev3 to your local box:

```bash
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/${VER} \
  ${VER}-${DATE}-${SEQ}
```

Copy from your local box to live2:

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

## 10. /latest/

If the build should also appear on /latest/ then update the `latest`
branch on GitHub, and repeat the steps above for VER=latest.
This is necessary because some aspects of the travis build depend on the
branch (e.g. to construct urls correctly).

## 11. (Minor/Major version only)  Update Apache config

See:

```
  salt/apache/ocds-docs-live.conf ("set live_versions = [...]")
  salt/ocds-docs/include/banner_* and version-options.html
```

## FAQ

**How can I find out what the standard looked like at 1.0?**

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

**How can I find out what the standard looked like at 1.1.0?**

TBC. (Is the answer to look for a tagged release?)
