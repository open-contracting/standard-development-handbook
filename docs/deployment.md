# Deployment

The section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.

## (1) Freeze extensions

Each release of the standard should pin to specific versions of each **core** extension. Community extensions are not pinned. 

This is currently achieved by:

* Creating a tagged release of each extension;
* Creating a tagged release of the extension registry that points to these specific versions;
* Setting the documentation build process to refer to the relevant extension registry tag;

### To pin extensions: worked example

For each [core extension](http://standard.open-contracting.org/latest/en/extensions/#core-extensions):

#### Review outstanding pull requests and changes since last release

1. Open the relevant repository in the Github web interface ([example](https://github.com/open-contracting/ocds_lots_extension))
1. Review any outstanding [pull requests](https://github.com/open-contracting/ocds_lots_extension/pulls) and discuss these to determine whether they should be merged before pinning the extension
1. Under the repository title and description, click **Releases** to view the list of existing releases ([example](https://github.com/open-contracting/ocds_lots_extension/releases))
1. Under the title of the most recent release, the number of commits since that release will be listed, if there are no commits since the last release then skip to 'Publish a new release', otherwise click the link to view the list of changes since the last release ([example](https://github.com/open-contracting/ocds_lots_extension/compare/v1.1...master))
1. Check the list of changes since the last release against the [changelog](http://standard.open-contracting.org/latest/en/schema/changelog/#changelog) for the version of OCDS being deployed
1. Before publishing the release, discuss any substantive changes, i.e. not simple typo or documentation updates, which aren't included in the changelog

#### Publish a new release

1. From the list of releases, click **Draft a new release**
1. In the 'Tag version' field, enter the version of OCDS being deployed in vmajor.minor.patch format, e.g. `v1.1.1`
1. In the 'Release title' field, enter a title, e.g. 'Fixed version for OCDS 1.1.1'
1. Enter a brief summary of changes, e.g. 'Typo fixes', and click **Publish release**

## (2) Merge standard

### Branch naming (ToMove)

A branch exists in the repository for each deployed (live) minor version of OCDS, named after the branch version. These version branches should be protected. 

For each version, a '-dev' branch may be created as the working copy. 

Patch versions may further branch off the '-dev' copy, with work merged into -dev before being merged into the live branch.

Worked example of branch structure:

* **1.0** - contains the latest deployed patch release of OCDS 1.0 (e.g. 1.0.2)
* **1.1** - contains the latest deployed patch release of OCDS 1.1 (e.g. 1.1.0)
  * **1.1-dev** - used to stage changes to version 1.1
  * **1.1.1-dev** - used to work on a 1.1.1 version

### Process

The -dev branch should be merged into the live branch for the version being deployed. 


## (3) Make validation schema

* Update standard/schema/make_validation_schema.py to refer to the correct version number (Line 94)
* Run make_validation_schema.py


## (4) Push updated translations

Run tx push -s
Run tx pull -a -f

## (5) Create a tagged release

Named e.g. 1__1__0


## (6) Copy the schema into place

See guidance at https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs-live.sls
If the 1.1 schema files were copied correctly, they should now appear at http://standard.open-contracting.org/schema/1__1__0/

## (7) FURTHER DEPLOYMENT STEPS



## Questions

**How can I find out what the standard looked like at 1.0?**

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

**How can I find out what the standard looked like at 1.1.0?**

TBC. (Is the answer to look for a tagged release?)

