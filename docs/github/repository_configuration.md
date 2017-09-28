# Repository configuration

1. Disable Wikis (or run [`rake repos:lint`](https://github.com/open-contracting/standard-maintenance-scripts))
1. If it is an extension, disable Issues and Projects (or run [`rake repos:lint`](https://github.com/open-contracting/standard-maintenance-scripts))
1. Add a description. The description should not describe the project's status ('draft'), because people frequently forget to update repository descriptions. Describe the status in the readme.
1. Add a website to the repository if relevant: for example, a link to a deployment of the tool or documentation.
1. [Protect](https://help.github.com/articles/about-protected-branches/) the default branch with these options (or run [`rake repos:protect_branches`](https://github.com/open-contracting/standard-maintenance-scripts)):

* Protect this branch
  * Require status checks to pass before merging
    * continuous-integration/travis-ci (if available)
  * Include administrators

We don't enable the following behaviors for the provided reasons:

* **Require branches to be up to date before merging**: While this may avoid introducing errors, it slows development in an environment in which there are many simultaneous pull requests, because each would require an extra step before merging. If the automated tests fail after merging, the error can be corrected, or the changes can be reverted.
* **Require pull request reviews before merging**: While this is a best practice, it slows development as the team is not sufficiently large to staff it. It is okay, for example, for an author to self-merge a simple change. Authors may, of course, request reviews for significant changes.
