# GitHub: Branch Management

Repositories should have only a default branch (usually `master`) and pull request branches. If the repository is a fork, it may have a `master` branch for the source branch and an `opencontracting` (or `open_contracting`) branch for the fork branch. The default branch should be [protected](https://help.github.com/articles/about-protected-branches/) with these options:

* Protect this branch
  * Require status checks to pass before merging
    * Require branches to be up to date before merging
    * continuous-integration/travis-ci (if available)
  * Include administrators

## Management Rules

* If a branch has no commits ahead of the default branch, and is merged, delete it.
* If a branch has no commits ahead of the default branch, and is not merged but is a month old, delete it.

## Expected non-default branches

* [standard](https://github.com/open-contracting/standard), starting with version 1.0, has an `X.X` branch for the production version of the documentation, and an `X.X-dev` branch for the development version of the documentation. It also has a `latest` branch, which must be kept up-to-date with the most recent `X.X` branch.
* [extension_registry](https://github.com/open-contracting/extension_registry), starting with version 1.1, has a branch for each minor or patch version of the standard and each profile. The only difference between the branches should be that the values of the `url` fields use a different tag name.

## Unexpected non-default branches

These should either be deleted, opened as pull requests, or protected and documented here.
