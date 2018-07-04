# Technical implementation of translation

This page documents the code involved in translating files. It is only necessary to read this page if you are editing or debugging these technical processes. Otherwise, the steps have been simplified and abstracted into the two commands `make extract` and `make`, covered under [Technical processes for translation](../technical) and [Building the documentation](../../technical/build).

```eval_rst
  .. note::
    We use the `gettext <https://en.wikipedia.org/wiki/Gettext>`_ system for translation. In gettext, strings to translate are referred to as 'messages', and messages are collected into 'domains', which correspond to POT files.
```

## Extract messages

First, strings to translate are extracted from files with `make extract`.

### Codelist CSV files and JSON Schema files

1. [`make extract`](https://github.com/open-contracting/standard_profile_template/blob/master/include/common.mk#L52-L53) builds the `extract_codelists` and `extract_schema` Make targets, among others. These run:

        pybabel extract -F .babel_codelists . -o $(POT_DIR)/$(DOMAIN_PREFIX)codelists.pot
        pybabel extract -F .babel_schema . -o $(POT_DIR)/$(DOMAIN_PREFIX)schema.pot

1. [`pybabel extract`](http://babel.pocoo.org/en/latest/cmdline.html#extract) extracts messages from source files and generates a POT file. The `-F` (`--mapping-file`) option sets the path to the Babel mapping configuration file, `.babel_codelists` or `.babel_schema`.

1. The [Babel mapping configuration files](http://babel.pocoo.org/en/latest/messages.html#extraction-method-mapping-and-configuration), `.babel_codelists` and `.babel_schema`, map Babel message extraction method names – `codelist_text` and `jsonschema_text` – to the codelist CSV files and JSON Schema source files from which to extract strings to translate.

1. [`setup.py` in `documentation-support`](https://github.com/open-contracting/documentation-support/blob/master/setup.py#L7-L11) maps the [Babel message extraction method names](http://babel.pocoo.org/en/latest/messages.html#writing-extraction-methods) to the module and function implementing the extraction, in the entry point group `babel.extractors`.

1. The functions [`extract_codelist` and `extract_schema` in `documentation-support`](https://github.com/open-contracting/documentation-support/blob/master/ocdsdocumentationsupport/babel_extractors.py) implement the extraction.

### Markdown files

1. `make extract` builds the `extract_markdown` Make target, among others. This runs:

        sphinx-build -q -b gettext $(DOCS_DIR) $(POT_DIR)

See the [Sphinx documentation](http://www.sphinx-doc.org/en/master/intl.html#sphinx-internationalization-details).

## Translate source files

After pushing strings to translate as POT files to Transifex, [translating the strings](../workflow), and pulling translations as PO files from Transifex, source files are translated with `make`.

### Codelist CSV files and JSON Schema files

1. [`make`](https://github.com/open-contracting/standard_profile_template/blob/master/include/common.mk#L122-L123) builds the `build.*` Make targets, among others. These run, for example:

        sphinx-build -q -b dirhtml $(DOCS_DIR) $(BUILD_DIR)/es -D language="es"

1. [`sphinx-build`](http://www.sphinx-doc.org/en/master/man/sphinx-build.html) runs `setup` in `conf.py`, which reads the `language` override (`-D language="es"`).

1. [`setup` in `conf.py`](https://github.com/open-contracting/standard_profile_template/blob/master/docs/conf.py#L139) calls the functions [`translate_codelists` and `translate_schema` in `documentation-support`](https://github.com/open-contracting/documentation-support/blob/master/ocds_documentation_support/translation.py) to translate codelist CSV files and JSON Schema files from one directory into another directory.

1. The translated files are used by Sphinx directives like `csv-table-no-translate` and `jsonschema` in Markdown files.

### Markdown files

1. `make` builds the `build.*` Make targets, among others. These run, for example:

        sphinx-build -q -b dirhtml $(DOCS_DIR) $(BUILD_DIR)/es -D language="es"

See the [Sphinx documentation](http://www.sphinx-doc.org/en/master/intl.html#sphinx-internationalization-details).
