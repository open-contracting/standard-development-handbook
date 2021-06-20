Common conventions
==================

This style guide covers our conventions when writing:

-  OCDS Schema and standard documentation
-  GitHub issues
-  Helpdesk responses
-  Associated presentations and documents

Readability
-----------

We strive to write concise, clear documentation. To improve your writing, please learn how to `write for the web <https://www.usa.gov/style-guide/writing-for-web>`__ (with many more resources at `Nielsen Norman Group <https://www.nngroup.com/topic/writing-web/>`__), and consider using these tools:

-  `Hemingway Editor <http://www.hemingwayapp.com/>`__
-  `Grammarly <https://www.grammarly.com/>`__
-  Readability statistics in Microsoft Word or `online tools <https://www.webfx.com/tools/read-able/flesch-kincaid.html>`__

Spelling
--------

Use American English (e.g. "organization" rather than "organisation") unless we are aligning a field name with an existing standard that uses alternative spellings. Notably, this means being careful about using "z" instead of "s" in many words of Latin origin.

Text formatting
---------------

-  When referring to a **field** or **codelist**, use the camelCase version of the field/codelist name, and enclose it in backticks so it is displayed in a montotype font as follows: ``camelCase``
-  When referring to a **building block**, use the capitalized CamelCase version of the building block name, and enclose it in backticks so it is displayed in a montotype font as follows: ``CamelCase``
-  When referring to a **code** from a codelist, enclose the value in single quotes, e.g. "We have added a 'direct' code to the ``method`` codelist"
-  When pluralizing a **field** or **building block**, treat the field/building block name as a proper noun, and add a ``'s`` instead of an ``s`` to the end, or treat it as a mass noun and add nothing to the end
-  When referring to a field in JSON Schema, use dot notation, like ``tender.id``. (Slash notation is reserved for `JSON Pointer <https://tools.ietf.org/html/rfc6901>`__. For example, the JSON Pointer for ``tender.id`` is ``/definitions/Tender/properties/id``.)
-  When referring to a field in OCDS data, use a JSON Pointer, like ``/tender/id``.

Word choice
-----------

-  "ocid" not "OCID". Although abbreviations in prose are uppercase, the mixing of upper- and lowercase in the documentation (when referring to the concept versus the field) may cause confusion.
-  "codelist" not "code-list" or "code list"
-  "changelog" not "change-log" or "change log"
-  "data package" not "datapackage"
-  "metadata" not "meta-data" or "meta data"
-  to describe the "-" character, "hyphen" not "dash" 

When describing JSON Schema:

-  "field" to refer to OCDS fields, like ``tender.id``
-  "property" to refer to JSON Schema metadata properties, like ``enum``
-  "array" not "list"
-  "object" not "block"
