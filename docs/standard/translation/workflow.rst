Translation workflow
====================

Roles
-----

A **Translator** translates the source content into one of the target languages. They must be familiar with the domain (public contracting and open data) and follow this handbook.

**Proofreaders** proofread translated text and focus on the quality of the writing (spelling, grammar and punctuation). They typically don't need to look at the source content.

**Reviewers** review the translated text to ensure it is *functional*. A functional translation enables a reader to access the same information and perform the same tasks as the source content would. Reviewers are domain experts and focus on the clarity of phrasing and usage of the glossary.

Translators, proofreaders and reviewers have excellent writing skills (spelling and grammar) and intervene only when the target language is their native language.

The **Release Manager** is responsible for the :doc:`../technical/deployment` of the new release of OCDS.

The **Coordinator** ensures good communication between the different roles.

Steps
-----

1. The Release Manager freezes source strings, i.e. no pull requests will be merged that change English strings in Markdown, JSON, CSV or ``.po`` files.
2. The Coordinator recruits the roles of translator, proofreader and reviewer and :ref:`gives access to the Transifex project<standard/translation/using_transifex:Control access permissions>`. Candidates are stored in a spreadsheet named "Roles in OCP translation processes" and in the CRM as contacts tagged "translator".
3. The Coordinator sends translators the links to the Transifex project and to this handbook.
4. When a Translator completes the translation of at least half the untranslated words, they contact the Proofreader with a link to the resource.
5. When a Proofreader completes the proofreading of at least half the unreviewed strings, they contact the Reviewer with a link to the resource.
6. Once a Reviewer has reviewed all unreviewed strings for all resources, they contact the Coordinator.

For the specific steps for each role to follow in Transifex, see :doc:`using_transifex`.
