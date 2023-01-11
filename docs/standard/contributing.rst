Contributing
============

This page describes the internal process for making changes to the standard repository.

Getting started
---------------

Before contributing to Markdown pages, read the :doc:`../../meta/style_guide`.

Before authoring a new documentation page, or extensively editing an existing page, read the `process note <https://docs.google.com/document/d/1vBn4HFaczjcCur19kSwEMwk2uciFCdNgm9S9Ue_LnjY/>`__ on using Google Docs to collaboratively edit standard documentation.

Before contributing to JSON Schema and CSV codelists, read the :doc:`../../meta/schema_style_guide` and the `schema patterns <https://os4d.opendataservices.coop/patterns/schema/>`__ section of `ODS' Standards Lab <https://os4d.opendataservices.coop/>`__.

To get up to speed on OCDS standard development, you should be familiar with:

-  The standard itself

   -  `OCDS documentation <https://standard.open-contracting.org/>`__, in particular the schema and codelists
   -  `Extension Explorer <https://extensions.open-contracting.org/>`__

-  The policies it follows

   -  `Normative and non-normative content and changes policy <https://docs.google.com/document/d/1xjlAneqgewZvHh6_hwuQ98hbjxRcA2IUqOTJiNGcOf8/edit>`__
   -  `Translation and localization policy <https://standard.open-contracting.org/1.1/en/support/governance/#translation-and-localization-policy>`__
   -  `Semantic versioning <https://semver.org>`__

To improve your technical writing skills, consider taking `Google's Technical Writing Courses <https://developers.google.com/tech-writing>`__, which can be completed in a day.

Proposing changes
-----------------

For worked examples, see the `process note <https://docs.google.com/document/d/1Sp1sXVx99k-zdpNKE6kAwGkmyHG6KWCIaiZ1GYE_cOY/edit>`__. For all other changes:

#. Agree on a proposal in a GitHub issue.
#. Assign the issue to yourself, and move the issue's card to the *In progress* column.
#. Create a branch of the ``standard`` repo (not a branch of your fork) in which to make your changes.

   -  **Never** use normative words on guidance pages. Use `non-normative synonyms <https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04#page-3>`__ instead.
   -  Consider composing Markdown content in `Hemingway Editor <http://www.hemingwayapp.com/>`__ or `Grammarly <https://www.grammarly.com/>`__, as suggested in the :doc:`../../meta/style_guide`.
   -  After adding a definition to ``release-schema.json``, add a sub-heading for the new sub-schema in ``reference.md``.
   -  After editing  ``release-schema.json`` or ``meta-schema-patch.json``, run:

      .. code-block:: bash

         python manage.py pre-commit

      .. admonition:: One-time setup

         .. code-block:: bash

            pip install -r requirements.txt

#. Update the **changelog**, maintaining schema order in the list of changes.
#. Commit your changes.

   .. admonition:: Atomic changes

      Make atomic changes in one commit, rather than over many commits: for example, when adding a definition to the schema, add it to the schema reference documentation in the same commit. That way, reverting a commit doesn't leave the standard in an incoherent state.

   .. admonition:: Commit messages

      Use the following format for commit messages:

      .. code-block:: none

         scope: Capitalized, <72 characters, no period

         A longer description of paragraph text, as needed.

      For example:

      .. code-block:: none

         primer/releases_and_records: Use "JSON data" instead of "JSON text"

      The *scope* is based on which files were changed:

      * The changelog file: ``changelog``
      * One Markdown file (can include changes to example files): ``path/to/page``, for example: ``primer/index``
      * Many Markdown files in a single section: ``path/to/section``, for example: ``guidance/map``
      * One schema file (can include changes to reference pages): the name of the file without extension, for example: ``release-schema``

      Other, less-used scopes are:

      * ``build``: Changes to the build system (requirements files, ``include``, ``script``, ``Makefile``, ``*.cfg``, ``*.py``)
      * ``ci``: Changes to continuous integration (``.github/workflows``)
      * ``locale``: Changes to translations (``docs/locale``)
      * ``test``: Changes to tests (``tests``)
      * ``chore``: Any other change not warranting a changelog entry (e.g. renaming pages or fixing typographical errors, broken URLs, Markdown syntax, etc.)

      Most commits are made in pull requests, such that it's easy to find the discussion on GitHub. As such, it's not necessary to provide a long narrative, if it exists in a pull request or linked issue.

      Reference:

      - `Angular Commit Message Format <https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit-message-header>`__
      - `Conventional Commits <https://www.conventionalcommits.org/en/v1.0.0/>`__
      - `Write joyous git commit messages <https://joshuatauberer.medium.com/write-joyous-git-commit-messages-2f98891114c4>`__

#. Create a pull request.

   -  Reference the issue number in the pull requests' description.
   -  Set the *base* branch, e.g. ``1.2-dev`` for OCDS 1.2 or ``1.1-dev`` for OCD 1.1.
   -  Set the *milestone*, e.g. ``1.2.0`` for OCDS 1.2.

#. Assign a data support manager to review.

   -  See the next section for reviewer's instructions.
   -  If changes are requested, make the changes, then repeat this step.

#. Once approved by a data support manager, assign James to review.

   -  If changes are requested, make the changes, then repeat this step.

#. Once approved by James, you can merge it yourself.

Logging changes
---------------

#. Follow the :doc:`../../meta/changelog_style_guide`.
#. If a **codelist** is added, use the :ref:`versionadded<version-admonitions>` admonition to indicate the version in which it was added, in ``codelists.md``.
#. If a **code** is added, use the :ref:`versionchanged<version-admonitions>` admonition to indicate the version in which it was added, with the message "Added the 'newCode' code.", in ``codelists.md``.

   .. note::

      If the codelist is open and frequently updated (like document type, milestone type, classification scheme, party role) or if it is external (like currency from ISO 4217), skip this step.

#. If a **codelist** is deprecated, use the :ref:`deprecated<version-admonitions>` admonition to indicate the version in which it was deprecated, in ``codelists.md``.
#. If a **code** is deprecated, use the :ref:`deprecated<version-admonitions>` admonition to indicate the version in which it was deprecated, with the message "Deprecated the 'oldCode' code.", in ``codelists.md``.
#. If a **field** is added to the release schema, unless it is a major structural change like the ``parties`` array, don't add any admonition to ``reference.md``.
#. If a **field** is deprecated in the release schema, and if it has its own section in ``reference.md``, use the :ref:`deprecated<version-admonitions>` admonition to indicate the version in which it was deprecated.

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

#. Draft a JSON example with reasonable values
#. Check `other standards <https://lov.linkeddata.es/dataset/lov>`__ for potential models

`Architecture decision records <https://github.blog/2020-08-13-why-write-adrs/>`__:

.. toctree::
   :glob:

   adr/*
