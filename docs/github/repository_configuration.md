# Repository configuration

1. Add a description. The description should not describe the project's status ('draft'), because people frequently forget to update repository descriptions. Describe the status in the readme instead.
1. Add a website to the repository, if relevant: for example, a link to a deployment of the tool or to its documentation.

The `fix:lint_repos` and `fix:protect_branches` Rake tasks in [standard-maintenance-scripts]](https://github.com/open-contracting/standard-maintenance-scripts) otherwise normalize configurations.

We don't generally enable the following behaviors on protected branches for the provided reasons:

* **Require branches to be up to date before merging**: While this may avoid introducing errors, it slows development in an environment in which there are many simultaneous pull requests, because each would require an extra step before merging. If the automated tests fail after merging, the error can be corrected, or the changes can be reverted.
* **Require pull request reviews before merging**: While this is a best practice, it slows development as the team is not sufficiently large to staff it. It is okay, for example, for an author to self-merge a simple change. Authors may, of course, request reviews for significant changes.
