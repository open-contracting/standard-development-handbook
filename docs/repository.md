# Standard Repository

The repository for the standard for open contracting is developed and maintained by Open Contracting Partnership in [GitHub](https://github.com/open-contracting/standard/tree/master/standard).

The standard uses [semantic versioning](http://semver.org/), with versions following the _MAJOR.MINOR.PATCH_ name convention.

## Branch naming

Each deployed (live) minor version of OCDS is based on a repository branch named after the version. These version branches should be [protected](https://help.github.com/articles/about-protected-branches/).

On addition to that, for each version branch a new branch with _'-dev'_ appended to the name may be created as a working copy. Patch versions may further branch off the dev copy, with work merged into dev before being finallly merged into the live branch.

Worked example of branch structure:

* **1.0** - contains the latest deployed patch release of OCDS 1.0 (e.g. 1.0.2)
* **1.1** - contains the latest deployed patch release of OCDS 1.1 (e.g. 1.1.0)
  * **1.1-dev** - used to stage changes to version 1.1 (such as minor documentation changes)
  * **1.1.1-dev** - used to work on a 1.1.1 version (including schema changes and fixes)

## Repository structure

* [.tx/config](https://github.com/open-contracting/standard/blob/HEAD/.tx/config) - config file for transifex
* [standard/schema/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema) - schema related files
  * `*.json` - json schema files
  * [codelists/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/codelists) - codelist csvs
  * [tests/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/tests) - python tests of the JSON schema
  * [utils/](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/utils) - python scripts for working with the JSON schema and codelist CSVs
* [standard/docs/en](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en) - English documentation
  * `*.md` `*/*.md` - English documentation text
  * [conf.py](https://github.com/open-contracting/standard/blob/HEAD/standard/docs/en/conf.py) - configuration of the docs site
  * [_static](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/_static) - css and javascript for the docs site
  * [_templates](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/_templates) - Jinja templates for the docs site - these contain only small overrides, as [we have our own theme](https://github.com/open-contracting/standard_theme)
* [standard/docs/locale](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/locale) - translations
* [standard/assets](https://github.com/open-contracting/standard/tree/HEAD/standard/assets) - images for inclusion of the docs

Created by running a build (not checked in):

* `.ve/` - python virtualenv, containing all necessary dependencies
* `build/` - contains the copy of the docs website we have just built
* `standard/schema/codelists_translated/` `standard/docs/en/extensions/codelists_translated/` - translated CSV files used by the build process
