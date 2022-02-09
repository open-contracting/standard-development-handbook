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

Use American English (e.g. "organization" rather than "organisation") unless we are aligning a field name with an existing standard that uses alternative spellings. Notably, this means being careful about using "z" instead of "s" in many words of Latin origin.

Text formatting
---------------

-  Do not use constructions like "supplier(s)" or "the supplier (or suppliers)". The plural is fine, like "suppliers".
-  Do not use smart quotation marks like ``“ ” ‘ ’``. Use simple quotation marks like ``" '``.
-  When referring to a **field** or **codelist**, use the camelCase version of the field/codelist name, and enclose it in backticks so it is displayed in a montotype font as follows: ``camelCase``
-  When referring to a **building block**, use the capitalized CamelCase version of the building block name, and enclose it in backticks so it is displayed in a montotype font as follows: ``CamelCase``
-  When referring to a **code** from a codelist, enclose the value in single quotes, e.g. "We have added a 'direct' code to the ``method`` codelist". Note that ``true`` and ``false`` are not codes; they are boolean values.
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
-  "hyphen" not "dash", to describe the "-" character
-  Prefer "release" and "record" to "OCDS release" and "OCDS record", unless the latter are clearer in context

For organization roles:

-  "buyer or procuring entity" not "buyer" or "procuring entity", except if the sentence is specific to one role
-  "supplier" for the awardee of a contract
-  "tenderer" for the submitter of a bid
-  "potential supplier" for a potential participant in a contracting process
-  "unsuccessful tenderer" not "unsuccessful bidder"

For procurement concepts:

-  "planning process" not "planning stage"
-  "organization" not "party" or "entity", except in cases like "procuring entity" or "third party"
-  "bid" not "tender", which is already used to describe the opportunity or solicitation
-  Never refer to an "OCDS process", "OCDS contracting process" or "OCDS planning process". "contracting process" and "planning process" refer to real-world processes, never to their OCDS representation. In OCDS, there are only releases and records.

When describing data:

-  "publication" for the data source that persists across time
-  "collection" for the publication's data at a specific point in time
-  "JSON data" not "JSON document", to avoid confusion with the `documents` field

When describing JSON Schema:

-  "field" to refer to OCDS fields, like ``tender.id``
-  "property" to refer to JSON Schema metadata properties, like ``enum``
-  "array" not "list"
-  "object" not "block"

When referring to a field, prefer the notation for the path in the data, like ``contracts.period``, rather than the notation for the path in the schema, like ``Contract.period``.

These regular expressions can be used to find breaches of the style guide, accounting for false positives.

"party" or "entity"
  ``(?<!curing| third)[^`-]\b(part|entit)(y|ies)\b[^"/`](?!array)``
"tender"
  ``a tender\b(?! (process|release))|submi(\S+ ){1,3} tender|tender submi``
"property"
  ``(?<!(`minLength| `required|geStrategy)` )propert(y|ies)``
data path notation
  ``\b[A-Z][a-zA-Z]+\.(?!(aspx|db|html|md|org|xml|zip)\b)[a-zA-Z]{2,}``

JSON example filenames
----------------------

#. Name the JSON example with a descriptive, lower-case filename, with underscores between words. If the file contains a specific release tag, such as a 'tenderUpdate', it is fine to use it as the filename.
#. Store the example in the ``docs/examples`` directory in the standard's repository. Create a sub-directory to group related examples, if one doesn't exists already, rather than using a common prefix to the filename.
#. If you need to make a file downloadable, use the download role, e.g.: {download}`link text <path/to/file>`, and don't place the file under ``docs/_static/``.

Images
------

#. Create the image, preferably using easily accessible collaborative tools like `Google Drawings <https://docs.google.com/drawings/>`__.
#. Store the editable version in the *Assets* folder within the appropriate folder within `this Google Drive folder <https://drive.google.com/drive/u/1/folders/1VBb7OaF8CAOrwuNL413pnNYDwv-MoJoo>`__.
#. Export the image in PNG format.
#. Use a descriptive, lower-case filename, with underscores between words. Append "_es" to the filename if the content is in Spanish.
#. Store the exported version in the ``docs/_static/png`` directory in the standard's repository. Create a sub-directory to group related images, as needed, rather than using a common prefix to the filename.
