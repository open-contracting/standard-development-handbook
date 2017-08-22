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
