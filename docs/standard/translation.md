# Translation

To support wide adoption, the Open Contracting Data Standard schema, codelists and documentation can be translated from their canonical English language version. Translations are maintained using Transifex.

This page describes the processes for translators. The steps required to include translations in a documentation build are described in the [technical processes section](technical/index).

## Translation projects

There are a number of OCDS related projects on Transifex:

* [Standard 1.0](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-0/dashboard/)
* [Standard 1.1](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/dashboard/)
* [Standard Theme](https://www.transifex.com/OpenDataServices/open-contracting-standard-theme/dashboard/) - containing the documentation theme
* [CoVE](https://www.transifex.com/OpenDataServices/cove/dashboard/) - containing the text for the the validator

### Standard 1.0/1.1

As you can see at [[1]](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/language/es/) there are multiple resources, these are:

['schema'](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/schema/76882756)

This takes the [4 JSON schema files](https://github.com/open-contracting/standard/tree/1.1-dev/standard/schema) and is used to generate the tables on the [schema reference page](http://standard.open-contracting.org/1.1-dev/es/schema/reference/) and the schema viewer for [release](http://standard.open-contracting.org/1.1-dev/es/schema/release/), [release packages](http://standard.open-contracting.org/1.1-dev/es/schema/release_package/), [records](http://standard.open-contracting.org/1.1-dev/es/schema/records_reference/) and [record packages](http://standard.open-contracting.org/1.1-dev/es/schema/record_package/), as well as the linked JSON Schema files.

['codelists'](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/codelists/76986036)

This takes the [codelist CSVs](https://github.com/open-contracting/standard/tree/1.1-dev/standard/schema/codelists) and outputs [codelist tables](http://standard.open-contracting.org/1.1-dev/es/schema/codelists/).

#### Standard Documentation

All the rest of the resources are one resource per markdown documentation file.

The originals are in [the docs/en folder ](https://github.com/open-contracting/standard/tree/1.1-dev/standard/docs/en)and provide the main content text at  <http://standard.open-contracting.org/1.1-dev/es/>

For example, [getting_started--publication_patterns](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/getting_started--publication_patterns/72743815) has a source of <https://github.com/open-contracting/standard/blob/1.1-dev/standard/docs/en/getting_started/publication_patterns.md> and is output at <http://standard.open-contracting.org/1.1-dev/es/getting_started/publication_patterns/>

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
