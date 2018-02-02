# Translation

This page describes processes for translators. The technical steps to push and pull translations from Transifex and to build translated schema, codelists and documentation are described under [translation technical processes](technical/translation).

## Languages

The two supported translations are:

* French
* Spanish

Community translations exist to various levels of completion.

## Translators, proofreaders and reviewers

```eval_rst
  .. todo::
    Describe the process for selecting translators and reviewers and managing permissions.
```

Translators, proofreaders and reviewers have excellent writing skills (spelling and grammar) and intervene only when the target language is their native language.

**Translators** write the source content in one of the target languages. They must be familiar with the topics (public contracting and data) and apply the guidelines (this document) and terminology (in Transifex) provided by the Open Contracting Partnership.

**Proofreaders** proofread the translation and focus on the quality of the writing: spelling, grammar, punctuation. They normally don't need to look at the source content.

**Reviewers** review the translation to ensure it is functional. A functional translation enables the reader to access the same information and perform the same tasks as the source document would. Reviewers are specialists of the domains at hand (public contracting and data) and focus on the clarity of the phrasing and the good usage of the terminology.

## Using Transifex

Translators use Transifex to translate the Open Contracting Data Standard schema, codelists and documentation from the source language, English, to other languages.

### Projects and resources

Transifex is organized into projects:

* [Standard 1.0](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-0/dashboard/)
* [Standard 1.1](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/dashboard/)
* [Standard Theme](https://www.transifex.com/OpenDataServices/open-contracting-standard-theme/dashboard/): strings from the documentation theme
* [CoVE](https://www.transifex.com/OpenDataServices/cove/dashboard/): strings from the OCDS Validator

Projects contain [resources](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/content/), which contain strings to be translated. Here, we discuss only Standard 1.0 and Standard 1.1.

With the exceptions of the `schema` and `codelists` resources, each resource sources its strings to be translated from a single Markdown (`.md`) documentation file in the [`standard/docs/en`](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en) directory tree. These files provide the content for <http://standard.open-contracting.org/latest/en/>.

For example, the resource [`getting_started--contracting_process`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/getting_started--contracting_process/111787219) sources strings from [`standard/docs/en/getting_started/contracting_process.md`](https://github.com/open-contracting/standard/blob/HEAD/standard/docs/en/getting_started/contracting_process.md) and provides the content for <http://standard.open-contracting.org/latest/es/getting_started/contracting_process/>.

```eval_rst
  .. note::
    The strings to be translated are extracted from the Markdown files in that directory tree by ``sphinx-build`` using the ``gettext`` builder. The Markdown files are later compiled by ``sphinx-build`` using the ``dirhtml`` builder to generate the `documentation pages <http://standard.open-contracting.org/latest/en/>`_ for each language.
```

For the [`codelists`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/codelists/76986036) resource, the strings to be translated are extracted from the CSV files in [`schema/codelists/*.csv`](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/codelists) and [`docs/en/extensions/codelists/*.csv`](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/extensions/codelists). They provide the content for the codelist tables on the [codelists](http://standard.open-contracting.org/latest/es/schema/codelists/) and [building blocks](http://standard.open-contracting.org/latest/es/getting_started/building_blocks/) pages, and some extensions pages like [bids](http://standard.open-contracting.org/latest/es/extensions/bids/). The translated CSV files are not distributed with the documentation.

For the [`schema`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/schema/76882756) resource, the strings to be translated are extracted from the JSON files in [`standard/schema`](https://github.com/open-contracting/standard/tree/HEAD/standard/schema). They provide the content for: the JSON Schema tables on the [release reference](http://standard.open-contracting.org/latest/es/schema/reference/) and [records reference](http://standard.open-contracting.org/latest/es/schema/records_reference/) pages; the schema viewers on the [release schema](http://standard.open-contracting.org/latest/es/schema/release/), [release package schema](http://standard.open-contracting.org/latest/es/schema/release_package/) and [record package schema](http://standard.open-contracting.org/latest/es/schema/record_package/) pages, and the translated JSON Schema files distributed with the documentation.

```eval_rst
  .. note::
    The strings are extracted from CSV and JSON files using the custom Babel extraction methods `codelists_extract <https://github.com/open-contracting/standard/blob/HEAD/standard/schema/utils/codelists_extract.py>`_ and `jsonschema_extract <https://github.com/open-contracting/standard/blob/HEAD/standard/schema/utils/jsonschema_extract.py>`_.

    The CSV and JSON files are then translated by the Python scripts `translate_codelists.py <https://github.com/open-contracting/standard/blob/HEAD/standard/schema/utils/translate_codelists.py>`_ and `translate_schema.py <https://github.com/open-contracting/standard/blob/HEAD/standard/schema/utils/translate_schema.py>`_.

    The Sphinx directives used to render the translated codelist and JSON Schema files are ``jsonschema`` and ``csv-table-no-translate``.
```

### How-to

```eval_rst
  .. todo::
    Add guidance on how to use Transifex.
```

From the translation interface, type `?` to see a list of shortcuts.

### Untranslated words

The dashboard of a translation project reports the number of *strings* to translate, but translators must know the number of *words* to translate in order to estimate the time and cost. To get the number of words:

1. Open the translation project
1. Scroll to the list of languages and click "Translate" for a language
1. Click "All resources" at the bottom of the screen
1. Click "# untranslated" at the top of the screen
1. Check the box at the right of the search bar
1. See the number of words at the right of the screen

### Translation glossary

A translation glossary is [available](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/glossary/en/) (change the language code at the end of the URL to view the glossary in different languages). It can also be accessed from within the translation editor.

The glossary contains key terms that must be used consistently.

In our translation process, we encourage translators to:

1. Populate the glossary with suggested translations of its terms
1. Validate the translations with the nominated reviewer
1. Translate the rest of the documentation

### What not to translate

Some titles and descriptions of codes are copied from external sources and should be translated by those sources, not OCDS. These are tagged as `should_be_translated_upstream` and indicated by a small tag icon.

## Translation workflow

```eval_rst
  .. todo::
    Describe the workflow.
```

## See also

* Blog post: [Localising OCDS: translations, terminology and extensions](https://www.open-contracting.org/2016/07/26/localising-ocds-translations-terminology-extensions/)
