# Repository configuration

1. Disable Wikis (or run [`rake repos:lint`](https://github.com/open-contracting/standard-maintenance-scripts))
1. If it is an extension, disable Issues and Projects (or run [`rake repos:lint`](https://github.com/open-contracting/standard-maintenance-scripts))
1. Add a description. The description should not describe the project's status ('draft'), because people frequently forget to update repository descriptions. Describe the status in the readme.
1. Add a website to the repository if relevant: for example, a link to a deployment of the tool or documentation.
1. [Protect](https://help.github.com/articles/about-protected-branches/) the default branch with these options (or run [`rake repos:protect_branches`](https://github.com/open-contracting/standard-maintenance-scripts)):

* Protect this branch
  * Require status checks to pass before merging
    * Require branches to be up to date before merging
    * continuous-integration/travis-ci (if available)
  * Include administrators
