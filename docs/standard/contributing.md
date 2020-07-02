# Contributing

This page describes the internal process for making changes to the standard repository.

## Getting started

Before contributing to Markdown pages, read the [Style Guide](../../meta/style_guide).

Before authoring a new documentation page, or extensively editing an existing page, read the [process note](https://docs.google.com/document/d/1vBn4HFaczjcCur19kSwEMwk2uciFCdNgm9S9Ue_LnjY/) on using Google Docs to collaboratively edit standard documentation.

Before contributing to JSON Schema and CSV codelists, read the [Schema Style Guide](../../meta/schema_style_guide) and the [schema patterns](https://os4d.opendataservices.coop/patterns/schema/) section of [ODS' Standards Lab](http://os4d.opendataservices.coop/).

To get up to speed on OCDS standard development, you should be familiar with:

* The standard itself
  * [OCDS documentation](https://standard.open-contracting.org/), in particular the schema and codelists
  * [Extension Explorer](https://extensions.open-contracting.org/)
* The policies it follows
  * [Normative and non-normative content and changes policy](https://docs.google.com/document/d/1xjlAneqgewZvHh6_hwuQ98hbjxRcA2IUqOTJiNGcOf8/edit)
  * [Translation and localization policy](https://standard.open-contracting.org/1.1/en/support/governance/#translation-and-localization-policy)
  * [Extension classification policy](https://docs.google.com/document/d/1zvR1PDefO6yTK28uKA6XCnxMLiC9oiEeb3uFjHuRyqI/edit) (draft)
  * [Semantic versioning](https://semver.org)

## Proposing changes

For worked examples, see the [process note](https://docs.google.com/document/d/1Sp1sXVx99k-zdpNKE6kAwGkmyHG6KWCIaiZ1GYE_cOY/edit). For all other changes:

1. Agree on a proposal in a GitHub issue.
1. Assign the issue to yourself, and move the issue's card to the *In progress* column.
1. Create a pull request, and reference the issue number in the pull requests' description.
    * As suggested in the [Style Guide](../../meta/style_guide), consider composing Markdown content in [Hemingway Editor](http://www.hemingwayapp.com/) or [Grammarly](https://www.grammarly.com/).
    * **Never** use normative words on guidance pages. Use [non-normative synonyms](https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04#page-3) instead.
1. Assign a helpdesk analyst to review.
    * See the next section for reviewer's instructions.
1. If changes are requested, make the changes, then repeat step 3.
1. Otherwise, assign James to review.

## Reviewing changes

You can use [this feature](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/reviewing-proposed-changes-in-a-pull-request) to suggest changes directly.

You should check for:

* **Correctness**: Do the changes conform to the standard and its principles?
* **Style**: Do the changes respect the [Style Guide](../../meta/style_guide) and [Schema Style Guide](../../meta/schema_style_guide)? Are [normative words](https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04#page-3) used on guidance pages?
* **Spelling and grammar**: If there are few errors, suggest changes directly. If there are many errors, ask the author to use Grammarly or similar.

## Repository management

### Issues

* [All issues](https://github.com/open-contracting/standard/issues?q=is%3Aissue+is%3Aopen+no%3Alabel) should be assigned one or more [labels](https://github.com/open-contracting/standard/labels).

### Milestones

* Each development version should have a milestone, like `1.1.5`, `1.2.0` or `2.0.0`. There should at most one milestone for each of the patch, minor and major levels.
* [All issues](https://github.com/open-contracting/standard/issues?q=is%3Aissue+is%3Aopen+no%3Amilestone+-label%3A%22Focus+-+Extensions%22+-label%3A%22Extensions+-+Local%22) should be assigned a [milestone](https://github.com/open-contracting/standard/milestones), unless they have the label *Focus - Extensions* or *Extensions - Local*.
* [Issues labelled *Extensions - Drafted*](https://github.com/open-contracting/standard/issues?q=is%3Aopen+is%3Aissue+label%3A%22Extensions+-+Drafted%22+-label%3A%22Extensions+-+Local%22+-milestone%3A%22Extension+Explorer%22+) should be assigned the *Extension Explorer* milestone, unless they have the label *Extensions - Local*.
* Non-normative issues should be assigned either the *Worked examples* or *Iterative improvements* milestone.

### Projects

* Each development version under active development should have a [organization-wide project](https://github.com/orgs/open-contracting/projects) using the *Automated kanban with reviews* template and linked to the `standard`, `ocds-extensions` and `extension-explorer` repositories.
