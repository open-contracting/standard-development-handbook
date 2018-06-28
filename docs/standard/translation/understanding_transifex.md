# Understanding Transifex

Translators use Transifex to translate the standard's schema, codelists and documentation from the source language (English) to other languages.

## Projects and resources

Transifex is organized into projects:

* [Standard 1.0](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-0/dashboard/)
* [Standard 1.1](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/dashboard/)
* [Standard Theme](https://www.transifex.com/OpenDataServices/open-contracting-standard-theme/dashboard/): strings from the documentation theme
* [CoVE](https://www.transifex.com/OpenDataServices/cove/dashboard/): strings from the OCDS Validator

Projects contain [resources](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/content/), which contain strings to be translated. Here, we discuss only Standard 1.0 and Standard 1.1.

## Strings to be translated

### From Markdown files

With the exceptions of the `schema` and `codelists` resources, each resource sources its strings to be translated from a single Markdown (`.md`) documentation file in the [`standard/docs/en`](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en) directory tree. These files provide the content for <http://standard.open-contracting.org/latest/en/>.

For example, the resource [`getting_started--contracting_process`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/getting_started--contracting_process/111787219) sources strings from [`standard/docs/en/getting_started/contracting_process.md`](https://github.com/open-contracting/standard/blob/HEAD/standard/docs/en/getting_started/contracting_process.md) and provides the content for <http://standard.open-contracting.org/latest/es/getting_started/contracting_process/>.

```eval_rst
  .. note::
    The strings to be translated are extracted from the Markdown files in that directory tree by ``sphinx-build`` using the ``gettext`` builder. The Markdown files are later used to generate the `documentation pages <http://standard.open-contracting.org/latest/en/>`_ for each language by ``sphinx-build`` using the ``dirhtml`` builder.
```

### From CSV and JSON files

For the [`codelists`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/codelists/76986036) resource, the strings to be translated are extracted from the CSV files in [`schema/codelists/*.csv`](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/codelists) and [`docs/en/extensions/codelists/*.csv`](https://github.com/open-contracting/standard/tree/HEAD/standard/docs/en/extensions/codelists). They provide the content for the codelist tables on the [codelists](http://standard.open-contracting.org/latest/es/schema/codelists/) and [building blocks](http://standard.open-contracting.org/latest/es/getting_started/building_blocks/) pages, and some extensions pages like [bids](http://standard.open-contracting.org/latest/es/extensions/bids/). The translated CSV files are not distributed with the documentation. [standard#673](https://github.com/open-contracting/standard/issues/673)

For the [`schema`](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/schema/76882756) resource, the strings to be translated are extracted from the JSON files in [`standard/schema`](https://github.com/open-contracting/standard/tree/HEAD/standard/schema). They provide the content for: the JSON Schema tables on the [release reference](http://standard.open-contracting.org/latest/es/schema/reference/) and [records reference](http://standard.open-contracting.org/latest/es/schema/records_reference/) pages; the schema viewers on the [release schema](http://standard.open-contracting.org/latest/es/schema/release/), [release package schema](http://standard.open-contracting.org/latest/es/schema/release_package/) and [record package schema](http://standard.open-contracting.org/latest/es/schema/record_package/) pages; and the translated JSON Schema files distributed with the documentation.

```eval_rst
  .. note::
    ``.babel_codelists`` identifies CSV files and ``.babel_schema`` identifies JSON files from which to extract strings to translate.

    The strings are extracted from these files using the custom Babel `extraction methods <https://github.com/open-contracting/documentation-support/blob/master/ocds_documentation_support/babel_extractors.py>`_ ``codelists_extract`` and ``jsonschema_extract``.

    The CSV and JSON files are then translated by the `Python methods <https://github.com/open-contracting/documentation-support/blob/master/ocds_documentation_support/translation.py>`_ ``translate_codelists`` and ``translate_schema``.

    The Sphinx directives used to render the translated codelist and JSON Schema files are ``jsonschema`` and ``csv-table-no-translate``.
```
