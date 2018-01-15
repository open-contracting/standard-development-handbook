# Documentation

Documentation is written in Markdown syntax with [recommonmark](https://recommonmark.readthedocs.org/en/latest/) building on [Commonmark](http://commonmark.org/)

## Non-normative changes

The following changes are permitted to a released version of the standard:

* Changes that produce no visible changes to outputs, the outputs being:
  * [standard.open-contracting.org](http://standard.open-contracting.org) HTML pages. If a change to a Markdown file results in no changes to translations, then that change is considered invisible.
  * CSV files (mostly codelists)
  * JSON files (mostly schema)
    * `release-schema.json`
    * `release-package-schema.json`
    * `record-package-schema.json`
    * `versioned-release-validation-schema.json`
    * `extension.json`
  * `LICENSE` and `LICENSE.md` files
* Whitespace changes that produce no visible changes to outputs. Indentation changes in JSON files are allowed.
* Typo fixes that result in no change to meaning or behavior. Fixing a typo in a code in a codelist CSV file, or in a field name like `uniqueItems` in a JSON Schema file, would change behavior. Fixing typos in `description` columns or `description` fields wouldn't change behavior.
