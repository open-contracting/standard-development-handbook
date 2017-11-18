# Repository archival

Assets that are no longer supported should be archived.

1. Agree whether to archive the repository. The archived repositories presently include:
    * Superseded repositories (e.g. [json-merge-patch](OpenDataServices/json-merge-patch) supersedes [jsonmerge](https://github.com/open-contracting-archive/jsonmerge))
    * Abandoned extensions (e.g. [ocds-equityTransferCaps-extension](https://github.com/open-contracting-archive/ocds-equityTransferCaps-extension))
    * Merged changes to the core standard, expressed as extension repositories (`ocds_upgrade_###`)
    * Exploratory repositories from pre-1.0 and pre-2015
1. Scan the repository's open issues, milestones, pull requests and non-default branches in case any can be quickly closed, merged or deleted. Counter [GitHub's recommendation](https://help.github.com/articles/about-archiving-repositories/), open issues and pull requests indicate the development status of a repository, and should be left open.
1. Change the repository's description to describe the reason for archival. If the repository has been superseded, change it to "Superseded by [owner]/[repository]" and change the URL to the new repository's URL.
1. Run the [`fix:archive_repos REPOS=repo1,repo2`](https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration) task on the repository.
1. Move the archive to the `open-contracting-archive` organization.
1. [Archive](https://help.github.com/articles/about-archiving-repositories/) the repository through its settings.
1. Run the [`repos:badges`](https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration) task.
