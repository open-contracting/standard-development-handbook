# Standard repository

The repository for the Open Contracting Data Standard is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/standard).

The standard uses [semantic versioning](http://semver.org/), with versions following the _MAJOR.MINOR.PATCH_ name convention.

## Branch naming

Each deployed (live) minor version of the standard's documentation is built from a branch named after the version, like `1.0`. These live branches should be [protected](https://help.github.com/articles/about-protected-branches/).

For each live branch, there is a branch with a _'-dev'_ suffix serving as a working copy. Patch versions may further branch off the dev branch, with work merged into the dev branch before finally being merged into the live branch.

Worked example of branch structure:

* **1.0**: contains the latest deployed patch release of OCDS 1.0 (e.g. 1.0.2)
* **1.1**: contains the latest deployed patch release of OCDS 1.1 (e.g. 1.1.0)
  * **1.1-dev**: used to stage changes to version 1.1 (such as minor documentation changes)
  * **1.1.1-dev**: used to work on a 1.1.1 version (including schema changes and fixes)

## Repository structure

* [.tx/config](https://github.com/open-contracting/standard/blob/HEAD/.tx/config): configuration of Transifex
* [standard/schema/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema): schema-related files
  * `*.json`: JSON Schema files
  * [codelists/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/codelists): codelist CSV files
  * [tests/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/tests): Python tests of the JSON Schema files
  * [utils/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/utils): Python scripts for working with the JSON Schema and codelist CSV files
* [standard/docs/en](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en): English documentation
  * `*.md` `*/*.md`: English documentation text
  * [conf.py](https://github.com/open-contracting/standard/blob/HEAD/standard/docs/en/conf.py): configuration of ReadTheDocs
  * [\_static](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/_static): CSS and JavaScript for the documentation
  * [\_templates](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/_templates): Jinja templates for the documentation (these contain only small overrides, as [we have our own theme](https://github.com/open-contracting/standard_theme))
* [standard/docs/locale](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/locale): translations of the English documentation
* [standard/assets](https://github.com/open-contracting/standard/tree/HEAD/standard/assets): images used in the documentation

The following files are created by running a build and are not version controlled:

* `.ve/`: Python virtualenv, containing all dependencies
* `build/`: contains the built copy of the documentation website
* `standard/schema/codelists_translated/` `standard/docs/en/extensions/codelists_translated/`: translated CSV files used in the build process
