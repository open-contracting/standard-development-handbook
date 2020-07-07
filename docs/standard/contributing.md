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

## Modelling approaches

Before proposing new structures:

1. Draft a JSON example with reasonable values
1. Check [other standards](https://lov.linkeddata.es/dataset/lov) for potential models

### Implicit sub-classes

Let's say we are modeling automobiles. Consider two options:

1. One class for Automobile, with a single set of properties, like manufacturer, model, color, etc.
2. One class per manufacturer, each with its own set of properties.

Which is better? Cars from different manufacturers have more commonalities than differences. (1) is better, because it better ensures standardization of property names across Automobile instances, which eases comparability.

Do contracting procedures have more commonalities than differences? We believe so. To promote standardization and comparability, it is better to use the same class for all procedures, as much as possible.

That said, there are differences. To model differences, instead of choosing between different classes, there are several options that better achieve standardization:

1. Have one "big" class that has all properties for all procedures.
  * This is simple for data users, as they only need to look up the reference for one class, and the same concept is always expressed using the same property of that one class. It also ensures standardization, since there is no possibility of two classes having different properties for the same concept.
  * This, of course, also makes it possible for data to be incoherent (e.g. publishing a justification for a direct award, as part of an open procedure). Systems would need rules to ensure data is not incoherent – but systems always need some rules, e.g. to ensure start dates are before end dates. With this option, they'll simply need more.

1. Have a "basic" class with properties common to all/most procedures, with subclasses for specific procedures.
  * Let's say we are also modelling motorcycles. We could have one "big" class for vehicles. If our use case is counting all the vehicles in use in a region, as part of an analysis to support transport decisions, this option works. If our use case is selling vehicles, it's better to have separate classes with different properties for motorcycles and cars, given that most buyers are either looking for one or the other and are not comparing between the two. Standardizing, e.g. fuel efficiency and carbon emissions, across both classes is not important to this use case (though it is relevant to the first use case).
  * This option is often chosen by semantic 'purists'. It strikes a different balance between the correctness and complexity of the model. For contracting, it segments different procedures into different classes, giving a feeling of having a clean model. However, it also opens the door to subclasses diverging over time. For example, for government leases, one might choose the terms "lessor" and "lessee". However, these terms are modeling the same concepts as "buyer" and "supplier" or "contracting authority" and "economic operator." If every procedure uses its own jargon for the same concepts, standardization is weaker and use is harder.
  * In practice, once data is serialized, this option often looks the same as (1). In terms of serialization, you can either:
      1. Introduce instances of different classes using different keys. Instead of `"tender": {…}` you'd have `"openProcedure": {…}`, `"directAward": {…}`, etc. This is bad, because data users now need to learn however many classes a given publisher implements. Instead of there being one place to find the submission period, there might be a dozen.
      1. Introduce instances of different classes (with the same superclass) using the *same* key. That is: `"tender": {…}` for all procedures. Some objects will have different fields because they are instances of different classes. The data will look the same as in (1) (as long as there have been no divergences between classes). To preserve the class information, a single field can indicate the class name, e.g. `"procedureType": "directAward"`; this can equally be done in (1) with a change in perspective: describing the procedure type rather than preserving the class name.
  * Given that, in practice, this option looks the same in JSON as (1), the only reason for pursuing it is to satisfy a desire for purity in modeling.

1. Have different classes for different procedures, with no class hierarchy.
  * This is the worst option, because it offers no mechanism to ensure any degree of standardization across classes.

An important point is that having no standardization at all offers the maximum flexibility (e.g. everyone uses whatever terms they like); standardization is about reducing flexibility, and the challenge is to find a way to do so without limiting use cases.

