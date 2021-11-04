Translation workflow
====================

.. _glossary:

Glossary
--------

A small number of key terms must be translated consistently. The `Transifex glossary <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/glossary/en/>`__ is used to trigger :ref:`warnings<view-translations-with-warnings>` when terms are not translated as expected. The glossary is `managed <https://docs.google.com/spreadsheets/d/171VRailLhqC3Pmw3Qkh4lIgUkmtSa7t4H2h7yntSZg8/edit#gid=0>`__ in Google Sheets and `uploaded <https://docs.transifex.com/glossary/uploading-an-existing-glossary>`__ to Transifex.

.. _roles:

Roles
-----

A **Translator** translates the source content into one of the target languages. They must be familiar with the domain (public contracting and open data), follow this handbook, and use the Transifex glossary.

**Proofreaders** proofread translated text and focus on the quality of the writing (spelling, grammar and punctuation). They typically don't need to look at the source content.

**Reviewers** review the translated text to ensure it is *functional*. A functional translation enables a reader to access the same information and perform the same tasks as the source content would. Reviewers are domain experts and focus on the clarity of phrasing and usage of the Transifex glossary.

Translators, proofreaders and reviewers have excellent writing skills (spelling and grammar) and intervene only when the target language is their native language.

The **Release Manager** is responsible for the :doc:`../technical/deployment` of the new release of OCDS.

The **Coordinator** ensures good communication between the different roles.

Steps
-----

#. The Release Manager freezes source strings, i.e. no pull requests will be merged that change English strings in Markdown, JSON, CSV or ``.po`` files.
#. The Coordinator recruits the roles of translator, proofreader and reviewer and :ref:`gives access to the Transifex project<standard/translation/using_transifex:Control access permissions>`. Candidates are stored in a spreadsheet named "Roles in OCP translation processes" and in the CRM as contacts tagged "translator".
#. The Coordinator sends translators the links to the Transifex project and to this handbook.
#. When a Translator completes the translation of at least half the untranslated words, they contact the Proofreader with a link to the resource.
#. When a Proofreader completes the proofreading of at least half the unreviewed strings, they contact the Reviewer with a link to the resource.
#. Once a Reviewer has reviewed all unreviewed strings for all resources, they contact the Coordinator.

For the specific steps for each role to follow in Transifex, see :doc:`using_transifex`.
