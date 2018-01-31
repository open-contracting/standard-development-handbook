# Translation

To support wide adoption, the Open Contracting Data Standard schema, codelists and documentation can be translated from their canonical English language version. Translations are maintained using Transifex.

This page describes the processes for translators. The steps required to include translations in a documentation build are described in the [technical processes section](technical/index).

## Translation projects

There are a number of OCDS related projects on Transifex:

* [Standard 1.0](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-0/dashboard/)
* [Standard 1.1](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/dashboard/)
* [Standard Theme](https://www.transifex.com/OpenDataServices/open-contracting-standard-theme/dashboard/) - containing the documentation theme
* [CoVE](https://www.transifex.com/OpenDataServices/cove/dashboard/) - containing the text for the the validator

## Languages

We currently actively maintain translations to:

* Spanish
* French

A number of other community translations exist in various levels of completion.

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

### How-to

```eval_rst
  .. todo::
    Add guidance on how to use Transifex.
```

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
