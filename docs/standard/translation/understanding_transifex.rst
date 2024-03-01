Understanding Transifex
=======================

Translators use Transifex to translate the strings in the standard's schema, codelist and documentation files from the source language (English) to other languages.

Projects and resources
----------------------

Transifex is organized into projects, like `OCDS 1.1 <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/dashboard/>`__. Projects contain `resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/content/>`__, which contain strings to be translated.

Strings to be translated
------------------------

From CSV and JSON files
~~~~~~~~~~~~~~~~~~~~~~~

Codelists
^^^^^^^^^

In OCDS, the strings in the `codelists <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/codelists/76986036>`__ resource are extracted from the CSV files in `schema/codelists/*.csv <https://github.com/open-contracting/standard/tree/HEAD/schema/codelists>`__. They provide the content for the codelist tables on the `codelists <https://standard.open-contracting.org/latest/es/schema/codelists/>`__ page.

In OC4IDS, the strings in the `infrastructure-codelists <https://app.transifex.com/open-contracting-partnership-1/oc4ids-09/infrastructure-codelists/>`__ resource are extracted from the CSV files in `schema/project-level/codelists/*.csv <https://github.com/open-contracting/infrastructure/tree/HEAD/schema/project-level/codelists>`__. They provide the content for the codelist tables on the `codelist reference <https://standard.open-contracting.org/infrastructure/latest/en/reference/codelists/>`__ page.

JSON Schema
^^^^^^^^^^^

In OCDS, the strings in the `schema <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/schema/76882756>`__ resource are extracted from the JSON files in `schema <https://github.com/open-contracting/standard/tree/HEAD/schema>`__. They provide the content for:

-  JSON Schema tables on the `release reference <https://standard.open-contracting.org/latest/es/schema/reference/>`__ and `records reference <https://standard.open-contracting.org/latest/es/schema/records_reference/>`__ pages
-  schema viewers on the `release <https://standard.open-contracting.org/latest/es/schema/release/>`__, `release package <https://standard.open-contracting.org/latest/es/schema/release_package/>`__ and `record package <https://standard.open-contracting.org/latest/es/schema/record_package/>`__ schema pages
-  translated JSON Schema files distributed with the documentation

In OC4IDS, the strings in the `infrastructure-schema <https://app.transifex.com/open-contracting-partnership-1/oc4ids-09/infrastructure-schema/>`__ resource are extracted from the JSON files in `schema <https://github.com/open-contracting/infrastructure/tree/HEAD/schema/project-level>`__. They provide the content for:

-  JSON Schema tables on the `schema reference <https://standard.open-contracting.org/infrastructure/latest/en/reference/schema/>`__ page
-  schema viewers on the `schema browser <https://standard.open-contracting.org/infrastructure/latest/en/reference/browser/>`__ and `packaging data <https://standard.open-contracting.org/infrastructure/latest/en/reference/package/>`__ pages.
-  translated JSON Schema files distributed with the documentation

OC4IDS mappings
^^^^^^^^^^^^^^^

In OC4IDS, the strings in the `infrastructure-mappings <https://app.transifex.com/open-contracting-partnership-1/oc4ids-09/infrastructure-mappings/>`__ resource are extracted from the CSV files in `mapping <https://github.com/open-contracting/infrastructure/tree/HEAD/mapping>`__. They provide the content for the mapping tables on the pages in the `CoST IDS and OCDS mapping <https://standard.open-contracting.org/infrastructure/latest/en/cost/>`__ section.

From Markdown files
~~~~~~~~~~~~~~~~~~~

With the exceptions of the above resources, each resource sources its strings to be translated from a single Markdown (``.md``) documentation file in the `docs <https://github.com/open-contracting/standard/tree/HEAD/docs>`__ directory tree. These files provide the content for https://standard.open-contracting.org/latest/en/.

For example, the resource `getting_started--contracting_process <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es/getting_started--contracting_process/111787219>`__ sources strings from `docs/getting_started/contracting_process.md <https://github.com/open-contracting/standard/blob/HEAD/docs/getting_started/contracting_process.md>`__ and provides the content for https://standard.open-contracting.org/latest/es/getting_started/contracting_process/.
