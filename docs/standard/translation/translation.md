# Translation

This page describes processes for translators. The technical steps to push and pull translations from [Transifex](understanding_transifex) and to build translated schema, codelists and documentation are described under the [translation technical processes](technical).

## Languages

The two supported translations are:

* French
* Spanish

Community translations exist to various levels of completion.

## Translators, proofreaders and reviewers

Translators, proofreaders and reviewers have excellent writing skills (spelling and grammar) and intervene only when the target language is their native language.

**Translators** write the source content in one of the target languages. They must be familiar with the topics (public contracting and data) and apply the guidelines (this document) and [terminology](terminology) (in Transifex) provided by the Open Contracting Partnership.

**Proofreaders** proofread the translation and focus on the quality of the writing: spelling, grammar, punctuation. They normally don't need to look at the source content.

**Reviewers** review the translation to ensure it is functional. A functional translation enables the reader to access the same information and perform the same tasks as the source document would. Reviewers are specialists of the domains at hand (public contracting and data) and focus on the clarity of the phrasing and the good usage of the terminology.

Candidates for these roles are stored in a spreadsheet named "Roles in OCP translation and terminology processes" and in the CRM as contacts tagged "translator".

## Translation workflow

For the specific steps that each role follows in Transifex, see the [steps for each role](using_transifex#steps-for-each-role).

1. The Release Manager freezes source strings, i.e. no pull requests will be merged that change English strings in Markdown, JSON, CSV or  `.po` files.
1. The Coordinator recruits people into the [roles](#translators-proofreaders-and-reviewers) of translator, proofreader and reviewer and [gives access to the Transifex project](using_transifex#controlling-access-permissions).
1. The Coordinator sends translators the links to the Transifex project and to this documentation page.
1. When a Translator completes the translation of at least half the untranslated words, they contact the Proofreader with a link to the resource.
1. When a Proofreader completes the proofreading of at least half the unreviewed strings, they contact the Reviewer with a link to the resource.
1. Once a Reviewer has reviewed all unreviewed strings for all resources, they contact the Coordinator.

The **Release Manager** is the person responsible for the deployment of the new release of OCDS. The role of **Coordinator** is comparable to that in the [terminology process](terminology#coordinator).

```eval_rst
  .. note::
    Some titles and descriptions of codes are copied from external sources and should be translated by those sources, not OCDS. These are tagged as ``should_be_translated_upstream`` and indicated by a small tag icon.
```

### Major and minor changes

A **major** change changes the meaning of a source string, requiring an update to the translation by a translator. A **minor** change doesn't change the meaning of a source string, but may require an update to the translation, e.g. to update a URL.

Transifex can't tell the difference, and the English author can't indicate which changes are major or minor before pushing to Transifex. Translators therefore don't know whether a string:

* is a new string that was never translated
* corresponds to a string that was translated, but now requires re-translation
* corresponds to a string that was translated, and only requires edits to e.g. URLs or formatting

In Transifex, the "Suggestions" tab displays similar source strings and their translations, along with a percent match, which can assist translators in assessing the situation, but this is a time-consuming task.

The English author should therefore go through the untranslated strings, identify the minor changes for which they are responsible, and, where possible, use the top suggestion (which should be over 95% match) and update it as needed (e.g. update a URL, change Markdown formatting).

Alternately, the English author can replicate the minor changes to the source strings in the translations in the `.po` files, and then push the translations to Transifex. See the important caveats under the [translation technical processes](technical#push-and-pull-translations-from-transifex).

```eval_rst
  .. note::
    ``sphinx-intl update -p POT_DIR -d LOCALE_DIR`` updates ``.po`` files based on ``.pot`` files. However, Transifex and ``sphinx-intl`` don't produce identical ``.po`` files, e.g.:

    - different ``wrapwidth`` (which is configurable in ``polib`` but not ``sphinx-intl``)
    - different headers
    - ``:0`` after filenames

    Thus, running ``sphinx-intl update`` results in a large diff. It's possible that pushing then pulling the ``.po`` files to and from Transifex could achieve a smaller diff.
```

## See also

* Blog post: [Localising OCDS: translations, terminology and extensions](https://www.open-contracting.org/2016/07/26/localising-ocds-translations-terminology-extensions/)
