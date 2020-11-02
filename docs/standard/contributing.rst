Contributing
============

This page describes the internal process for making changes to the standard repository.

Getting started
---------------

Before contributing to Markdown pages, read the :doc:`../../meta/style_guide`.

Before authoring a new documentation page, or extensively editing an existing page, read the `process note <https://docs.google.com/document/d/1vBn4HFaczjcCur19kSwEMwk2uciFCdNgm9S9Ue_LnjY/>`__ on using Google Docs to collaboratively edit standard documentation.

Before contributing to JSON Schema and CSV codelists, read the :doc:`../../meta/schema_style_guide` and the `schema patterns <https://os4d.opendataservices.coop/patterns/schema/>`__ section of `ODS’ Standards Lab <https://os4d.opendataservices.coop/>`__.

To get up to speed on OCDS standard development, you should be familiar with:

-  The standard itself

   -  `OCDS documentation <https://standard.open-contracting.org/>`__, in particular the schema and codelists
   -  `Extension Explorer <https://extensions.open-contracting.org/>`__

-  The policies it follows

   -  `Normative and non-normative content and changes policy <https://docs.google.com/document/d/1xjlAneqgewZvHh6_hwuQ98hbjxRcA2IUqOTJiNGcOf8/edit>`__
   -  `Translation and localization policy <https://standard.open-contracting.org/1.1/en/support/governance/#translation-and-localization-policy>`__
   -  `Extension classification policy <https://docs.google.com/document/d/1zvR1PDefO6yTK28uKA6XCnxMLiC9oiEeb3uFjHuRyqI/edit>`__ (draft)
   -  `Semantic versioning <https://semver.org>`__

To improve your technical writing skills, consider taking `Google’s Technical Writing Courses <https://developers.google.com/tech-writing>`__, which can be completed in a day.

Proposing changes
-----------------

For worked examples, see the `process note <https://docs.google.com/document/d/1Sp1sXVx99k-zdpNKE6kAwGkmyHG6KWCIaiZ1GYE_cOY/edit>`__. For all other changes:

1. Agree on a proposal in a GitHub issue.
2. Assign the issue to yourself, and move the issue’s card to the *In progress* column.
3. Create a branch of the ``standard`` repo (not a branch of your fork) in which to make your changes.

   -  As suggested in the :doc:`../../meta/style_guide`, consider composing Markdown content in `Hemingway Editor <http://www.hemingwayapp.com/>`__ or `Grammarly <https://www.grammarly.com/>`__.
   -  **Never** use normative words on guidance pages. Use `non-normative synonyms <https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04#page-3>`__ instead.

4. Commit your changes, as well as the following:

   -  If you edited the release schema, run ``python util/make_dereferenced_release_schema.py``
   -  If you added a field to the release schema, run ``python util/make_versioned_release_schema.py``
   -  Update the **changelog**.

5. Create a pull request.

   -  Reference the issue number in the pull requests’ description.
   -  Set the *base* branch, e.g. ``1.2-dev`` for OCDS 1.2 or ``1.1-dev`` for OCD 1.1.
   -  Set the *milestone*, e.g. ``1.2.0`` for OCDS 1.2.

6. Assign a helpdesk analyst to review.

   -  See the next section for reviewer’s instructions.
   -  If changes are requested, make the changes, then repeat this step.

7. Once approved by a helpdesk analyst, assign James to review.

   -  If changes are requested, make the changes, then repeat this step.

8. Once approved by James, you can merge it yourself.

Reviewing changes
-----------------

You can use `this feature <https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/reviewing-proposed-changes-in-a-pull-request>`__ to suggest changes directly.

You should check for:

-  **Correctness**: Do the changes conform to the standard and its principles?
-  **Style**: Do the changes respect the :doc:`../../meta/style_guide` and :doc:`../../meta/schema_style_guide`? Are `normative words <https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04#page-3>`__ used on guidance pages?
-  **Spelling and grammar**: If there are few errors, suggest changes directly. If there are many errors, ask the author to use Grammarly or similar.

Repository management
---------------------

Issues
~~~~~~

-  `All issues <https://github.com/open-contracting/standard/issues?q=is%3Aissue+is%3Aopen+no%3Alabel>`__ should be assigned one or more `labels <https://github.com/open-contracting/standard/labels>`__.

Milestones
~~~~~~~~~~

-  Each development version should have a milestone, like ``1.1.5``, ``1.2.0`` or ``2.0.0``. There should at most one milestone for each of the patch, minor and major levels.
-  `All issues <https://github.com/open-contracting/standard/issues?q=is%3Aissue+is%3Aopen+no%3Amilestone+-label%3A%22Focus+-+Extensions%22+-label%3A%22Extensions+-+Local%22>`__ should be assigned a `milestone <https://github.com/open-contracting/standard/milestones>`__, unless they have the label *Focus - Extensions* or *Extensions - Local*.
-  `Issues labelled Extensions - Drafted <https://github.com/open-contracting/standard/issues?q=is%3Aopen+is%3Aissue+label%3A%22Extensions+-+Drafted%22+-label%3A%22Extensions+-+Local%22+-milestone%3A%22Extension+Explorer%22+>`__ should be assigned the *Extension Explorer* milestone, unless they have the label *Extensions - Local*.
-  Non-normative issues should be assigned either the *Worked examples* or *Iterative improvements* milestone.

Projects
~~~~~~~~

-  Each development version under active development should have a `organization-wide project <https://github.com/orgs/open-contracting/projects>`__ using the *Automated kanban with reviews* template and linked to the ``standard``, ``ocds-extensions`` and ``extension-explorer`` repositories.

Modelling approaches
--------------------

Before proposing new structures:

1. Draft a JSON example with reasonable values
2. Check `other standards <https://lov.linkeddata.es/dataset/lov>`__ for potential models

`Architecture decision records <https://github.blog/2020-08-13-why-write-adrs/>`__:

.. toctree::
   :glob:

   adr/*
