# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.


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

(If required, this may happen by first merging a patch dev branch into the dev branch for a major or minor version, and then merging onwards into the live branch)


## 6. Create a tagged release

Named e.g. 1__1__0


## 7. Copy the schema into place

See guidance at [https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs-live.sls](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs-live.sls).
If the 1.1 schema files were copied correctly, they should now appear at [http://standard.open-contracting.org/schema/1__1__0/](http://standard.open-contracting.org/schema/1__1__0/).

## 8. Further deployment step (WIP)


## FAQ

**How can I find out what the standard looked like at 1.0?**

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

**How can I find out what the standard looked like at 1.1.0?**

TBC. (Is the answer to look for a tagged release?)
