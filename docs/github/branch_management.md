# Branch management

Repositories should have only a default branch (usually `master`) and pull request branches. If the repository is a fork, it may have a `master` branch for the source branch and an `opencontracting` (or `open_contracting`) branch for the fork branch.

## Protecting branches

The default branch should be [protected](https://help.github.com/articles/about-protected-branches/) as described under [repository configuration](repository_configuration). On the [`standard` repository](https://github.com/open-contracting/standard) are protected, the `latest`, `#.#` and `#.#-dev` branches are also protected.

It isn't possible to commit directly to protected branches. The overhead of opening a pull request for even minor changes like small typos is acceptable so far, considering pull request reviews are not required, and considering opening a pull request ensures that the build is never accidentally broken, as all pull requests are tested on Travis before merging. :issue:`22`

## Pruning branches

* After merging a pull request, delete its branch.
* If a branch has no commits ahead of the default branch, and is merged, delete it.
* If a branch has no commits ahead of the default branch, and is not merged but is a month old, delete it.

### Expected unprotected branches

* [standard](https://github.com/open-contracting/standard), starting with version 1.0, has an `X.X` branch for the production version of the documentation, and an `X.X-dev` branch for the development version of the documentation. It also has a `latest` branch, which must be kept up-to-date with the most recent `X.X` branch.
* [extension_registry](https://github.com/open-contracting/extension_registry), starting with version 1.1, has a branch for each minor or patch version of the standard and each profile. The only difference between the branches should be that the values of the `url` fields use a different tag name.

### Unexpected unprotected branches

Unprotected branches more than a month old should either be opened as pull requests, documented as expected unprotected branches, or deleted.
