Understanding Transifex
=======================

Translators use Transifex to translate the strings in the standard's schema, codelist and documentation files from the source language (English) to other languages.

Projects and resources
----------------------

Transifex is organized into projects, like `OCDS 1.1 <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/dashboard/>`__. Projects contain `resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/content/>`__, which contain strings to be translated.

Strings to be translated
------------------------

From Markdown files
~~~~~~~~~~~~~~~~~~~

With the exceptions of the ``schema`` and ``codelists`` resources, each resource sources its strings to be translated from a single Markdown (``.md``) documentation file in the `docs <https://github.com/open-contracting/standard/tree/HEAD/docs>`__ directory tree. These files provide the content for https://standard.open-contracting.org/latest/en/.

For example, the resource `getting_started--contracting_process <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/getting_started--contracting_process/111787219>`__ sources strings from `docs/getting_started/contracting_process.md <https://github.com/open-contracting/standard/blob/HEAD/docs/getting_started/contracting_process.md>`__ and provides the content for https://standard.open-contracting.org/latest/es/getting_started/contracting_process/.

From CSV and JSON files
~~~~~~~~~~~~~~~~~~~~~~~

For the `codelists <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/codelists/76986036>`__ resource, the strings to be translated are extracted from the CSV files in `schema/codelists/*.csv <https://github.com/open-contracting/standard/tree/HEAD/schema/codelists>`__. They provide the content for:

-  codelist tables on the `codelists <https://standard.open-contracting.org/latest/es/schema/codelists/>`__ page

For the `schema <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/schema/76882756>`__ resource, the strings to be translated are extracted from the JSON files in `schema <https://github.com/open-contracting/standard/tree/HEAD/schema>`__. They provide the content for:

-  JSON Schema tables on the `release reference <https://standard.open-contracting.org/latest/es/schema/reference/>`__ and `records reference <https://standard.open-contracting.org/latest/es/schema/records_reference/>`__ pages
-  schema viewers on the `release <https://standard.open-contracting.org/latest/es/schema/release/>`__, `release package <https://standard.open-contracting.org/latest/es/schema/release_package/>`__ and `record package <https://standard.open-contracting.org/latest/es/schema/record_package/>`__ schema pages
-  translated JSON Schema files distributed with the documentation
