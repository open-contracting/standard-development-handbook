# Standard repository

## Branches and tags

The standard uses [semantic versioning](http://semver.org/), with versions following the _MAJOR.MINOR.PATCH_ name convention.

Each minor version of the standard's documentation is built from a "live" branch named after the version, like `1.0`. For each live branch, there is a dev branch with a `-dev` suffix. Patch versions may further branch off the dev branch, with work merged into the dev branch before finally being merged into the live branch. [standard.open-contracting.org](https://standard.open-contracting.org/) redirects to (`https://standard.open-contracting.org/latest/en/`), which uses the `latest` branch, which [should be](deployment) the same as the most recent live branch; this makes it possible to link to the latest version of the documentation without specifying the version number.

Sample branch structure:

* **1.0**: contains the latest deployed patch release of OCDS 1.0 (e.g. 1.0.2)
* **1.1**: contains the latest deployed patch release of OCDS 1.1 (e.g. 1.1.0)
  * **1.1-dev**: used to stage changes to version 1.1 (such as minor documentation changes)
  * **1.1.1-dev**: used to work on a 1.1.1 version (including schema changes and fixes)

The `latest`, `X.X` and `X.X-dev` branches are [protected](https://help.github.com/articles/about-protected-branches/). The `standard` repository also protects non-existent `infrastructure` and `profiles` branches. These names match sub-directories on the server, and therefore must not be used for branches.

The published documentation has versions on different `MAJOR.MINOR` [branches](https://github.com/open-contracting/standard/branches/all) (e.g. <https://standard.open-contracting.org/1.0/en/>), whereas the published schema has versions on different `MAJOR__MINOR__PATCH` [tagged releases](https://github.com/open-contracting/standard/tags) (e.g. <https://standard.open-contracting.org/schema/1__0__1/release-schema.json>). This use of branches and tags allows documentation to change between versions, while ensuring schema isn't changed between versions.

## Structure

* [.tx/config](https://github.com/open-contracting/standard/blob/HEAD/.tx/config): configuration of Transifex
* [include/](https://github.com/open-contracting/standard/tree/HEAD/include): common makefiles for building documentation
* [assets/](https://github.com/open-contracting/standard/tree/HEAD/assets): images used in the documentation
* [docs/](https://github.com/open-contracting/standard/tree/HEAD/docs): English documentation
  * `*.md` `*/*.md`: English documentation text
  * [conf.py](https://github.com/open-contracting/standard/blob/HEAD/docs/conf.py): Sphinx configuration
  * [\_static/](https://github.com/open-contracting/standard/tree/HEAD/docs/_static): CSS and JavaScript for the documentation
  * [\_templates/](https://github.com/open-contracting/standard/tree/HEAD/docs/_templates): Jinja templates for the documentation (these contain only small overrides, as [we have our own theme](https://github.com/open-contracting/standard_theme))
  * [locale/](https://github.com/open-contracting/standard/tree/HEAD/locale): translations of the English documentation
* [schema/](https://github.com/open-contracting/standard/tree/HEAD/schema): schema-related files
  * `*.json`: JSON Schema files
  * [codelists/](https://github.com/open-contracting/standard/tree/HEAD/schema/codelists): codelist CSV files
  * [tests/](https://github.com/open-contracting/standard/tree/HEAD/schema/tests): Python tests of the JSON Schema files
* [tests/](https://github.com/open-contracting/standard/tree/HEAD/tests): Python tests of the built documentation
* [util/](https://github.com/open-contracting/standard/tree/HEAD/schema/utils): Python scripts, mainly for working with the JSON Schema and codelist CSV files

The following files are created by running a build and are not version controlled:

* `.ve/`: Python virtualenv, containing all dependencies
* `build/`: contains the built copy of the documentation website

To understand `babel_ocds_codelist.cfg` and `babel_ocds_schema.cfg`, see [Understanding Transifex](../translation/understanding_transifex).
