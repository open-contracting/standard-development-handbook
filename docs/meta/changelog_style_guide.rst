Changelog style guide
=====================

Use the following format::

   - [#<PR number>](<PR link>) <Description>

`<Description>` should begin with a capitalised verb and end with a period.

For example::

   - [#1237](https://github.com/open-contracting/standard/pull/1237) Add `Tender.selectionCriteria`.

Normative content
-----------------

-  Changelog entries should be descriptive.

   Bad entry
     Update merging specification.
   Good entry
     Add rules on setting ``id`` and ``date`` for compiled releases to the merging specification.

-  If changes are made to files under the ``schema`` directory, it is assumed that corresponding changes were made to files under the ``docs`` directory. Do not add an entry under the "Documentation" heading if the changes directly correspond to entries under the "Codelists" and/or "Schema" headings.

-  For changes to schema and codelists, preserve schema/codelist ordering when adding new changelog entries. Otherwise, to reduce merge conflicts, add new changelog entries to the end of the relevant bullet list.

Non-normative content
---------------------

Changelog entries should be descriptive. Do not add an entry like "Improve organizational unit example." Instead, simply add the PR number to the "Organizational units" list item.
