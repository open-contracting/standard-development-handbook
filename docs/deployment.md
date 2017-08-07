# Deployment

The section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch upgrades.

### Branch naming (ToMove)

A branch exists in the repository for each deployed (live) minor version of OCDS, named after the branch version. These version branches should be protected. 

For each version, a '-dev' branch may be created as the working copy. 

Patch versions may further branch off the '-dev' copy, with work merged into -dev before being merged into the live branch.

Worked example of branch structure:

* **1.0** - contains the latest deployed patch release of OCDS 1.0 (e.g. 1.0.2)
* **1.1** - contains the latest deployed patch release of OCDS 1.1 (e.g. 1.1.0)
  * **1.1-dev** - used to stage changes to version 1.1 (such as minor documentation changes)
  * **1.1.1-dev** - used to work on a 1.1.1 version (including schema changes and fixes)


## (1) Freeze extensions

Each release of the standard should pin to specific versions of each **core** extension. Community extensions are not pinned. 

This is currently achieved by:

* Creating a tagged release of each extension;
* Creating a tagged release of the extension registry that points to these specific versions;
* Setting the documentation build process to refer to the relevant extension registry tag;

### To pin extensions: worked example

ADD DOCUMENTATION HERE


## (2) Check schema IDs

Check that the `id` property at the top of each JSON schema file have been updated to reflect the current major__minor__patch version number. 

For example: 

```json
{
  "id": "http://standard.open-contracting.org/schema/1__1__1/record-package-schema.json",
  "$schema": "http://json-schema.org/draft-04/schema#"
}
```

## (3) Make validation schema

The 'versioned-release-validation-schema.json' file exists for validation of versioned releases. It is currently programatically generated from the latest version of the schema and committed to the repository. 

To run this script:

1. Update 'standard/schema/make_validation_schema.py' to refer to the correct version number (Line 94)
2. Run make_validation_schema.py

Then commit the updated 'versioned-release-validation-schema.json' file to the repository. 

## (4) Push and pull updated translations

Run `tx push -s` to push updated sources files to Transifex

Run `tx pull -a -f` to pull all updated translation files down locally.

Commit the updated translations to the repository. 

**ToDo**: How can we test translation and be sure all strings had valid translations? 

## (5) Merge standard

The '-dev' working branch should be merged into the relevant live branch. 

(If required, this may happen by first merging a patch '-dev' branch into the '-dev' branch for a major or minor version, and then merging onwards into the live branch)


## (6) Create a tagged release

Named e.g. 1__1__0


## (7) Copy the schema into place

See guidance at https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs-live.sls
If the 1.1 schema files were copied correctly, they should now appear at http://standard.open-contracting.org/schema/1__1__0/

## (7) FURTHER DEPLOYMENT STEPS



## Questions

**How can I find out what the standard looked like at 1.0?**

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

**How can I find out what the standard looked like at 1.1.0?**

TBC. (Is the answer to look for a tagged release?)

