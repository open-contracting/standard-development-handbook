Common conventions
==================

This style guide covers our conventions when writing:

-  OCDS Schema and standard documentation
-  GitHub issues
-  Data support responses
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
-  When referring to a **subschema**, use the capitalized CamelCase version of the subschema name, and enclose it in backticks so it is displayed in a montotype font as follows: ``CamelCase``
-  When referring to a **code** from a codelist, enclose the value in single quotes, e.g. "We have added a 'direct' code to the ``method`` codelist". Note that ``true`` and ``false`` are not codes; they are boolean values.
-  When pluralizing a **field** or **subschema**, treat the field/subschema name as a proper noun, and add a ``'s`` instead of an ``s`` to the end, or treat it as a mass noun and add nothing to the end
-  When referring to a field in JSON Schema, use dot notation, like ``tender.id``. (Slash notation is reserved for `JSON Pointer <https://tools.ietf.org/html/rfc6901>`__. For example, the JSON Pointer for ``tender.id`` is ``/definitions/Tender/properties/id``.)
-  When referring to a field in OCDS data, use a JSON Pointer, like ``/tender/id``.

Word choice
-----------

General
~~~~~~~

-  "example", **not** "worked example"
-  "user", **not** "data user"
-  "hyphen", **not** "dash", to describe the "-" character
-  "for example", "such as", "like" or "including", **not** "e.g."
-  "that is", "in other words" or "meaning", **not** "i.e."
-  **Never** use "free-text"

Data concepts
~~~~~~~~~~~~~

-  Use ``ocid`` to refer to the field and "OCID" to refer to the concept
-  "phase", **not** "stage", for parts of OCDS implementation
-  "changelog", **not** "change-log" or "change log"
-  "codelist", **not** "code-list" or "code list"
-  "data package", **not** "datapackage"
-  "metadata", **not** "meta-data" or "meta data"

When describing data:

-  "publication" for the data source that persists across time
-  "collection" for the publication's data at a specific point in time
-  "JSON data", **not** "JSON document", to avoid confusion with the ``documents`` field
-  Prefer "release" and "record" to "OCDS release" and "OCDS record", unless the latter are clearer in context

When describing JSON Schema:

-  "field" to refer to OCDS fields, like ``tender.id``
-  "property" to refer to JSON Schema metadata properties, like ``enum``
-  "array", **not** "list"
-  "object", **not** "block"

When referring to a field, prefer the notation for the path in the data, like ``contracts.period``, rather than the notation for the path in the schema, like ``Contract.period``.

Procurement concepts
~~~~~~~~~~~~~~~~~~~~

-  "organization", **not** "party" or "entity", except in cases like "procuring entity" or "third party"
-  "bid", **not** "tender", which is already used to describe the opportunity or solicitation
-  "stage", **not** "phase", for parts of a contracting process or framework agreement procedure
-  Use the order "goods", "services" and "works" (alphabetical)

Instead of "tender", which can mean both the bid from the supplier and the opportunity from the buyer:

-  "bid", when referring to a submission from a supplier
-  "opportunity" (or "procurement opportunity"), when referring to a request, contest, etc. from a buyer
-  "contracting process", when referring to the entire process
-  "tender stage", when referring to the part of the contracting process
-  "tender release", like in the context of release tags
-  "tender notice", like in the context of document types
-  "tender object", when referring to the field

Processes:

-  "contracting (or planning) process", unless the sentence relates to only one or the other
-  "(contracting or planning) process", if the sentence relates to a scope of uniqueness
-  "planning process", **not** "planning stage"
-  **Never** refer to an "OCDS process", "OCDS contracting process" or "OCDS planning process". "contracting process" and "planning process" refer to real-world processes, never to their OCDS representation. In OCDS, there are only releases and records.

Organization roles:

-  "buyer or procuring entity", **not** "buyer" or "procuring entity", except if the sentence is specific to one role, and **not** "contracting authority"
-  "supplier" for the awardee of a contract
-  "tenderer" for the submitter of a bid
-  "potential supplier" for a potential participant in a contracting process
-  "unsuccessful tenderer", **not** "unsuccessful bidder"

For maintainers
~~~~~~~~~~~~~~~

These regular expressions can be used to find breaches of the style guide, accounting for false positives.

"party" or "entity"
  ``(?<!curing| third)[^`-]\b(part|entit)(y|ies)\b[^"/`](?!array)``
"tender"
  ``a tender\b(?! (process|release))|submi(\S+ ){1,3} tender|tender submi``
"property"
  ``(?<!(`minLength| `required|geStrategy)` )propert(y|ies)``
data path notation
  ``\b[A-Z][a-zA-Z]+\.(?!(aspx|db|html|md|org|xml|zip)\b)[a-zA-Z]{2,}``

.. _json-example-filenames:

JSON example filenames
----------------------

#. Name the JSON example with a descriptive, lower-case filename, with underscores between words. If the file contains a specific release tag, such as a 'tenderUpdate', it is fine to use it as the filename.
#. Store the example in the ``docs/examples`` directory in the standard's repository. Create a sub-directory to group related examples, if one doesn't exists already, rather than using a common prefix to the filename.
#. If you need to make a file downloadable, don't place it in ``docs/_static/``, instead use the download role, e.g.:

.. code-block::

   {download}`link text <../../examples/file>`

extension.json metadata files
-----------------------------

-  Do not use backticks.

Images
------

#. Create the image, preferably using easily accessible collaborative tools like `Google Drawings <https://docs.google.com/drawings/>`__.
#. Store the editable version in the *Assets* folder within the appropriate folder within `this Google Drive folder <https://drive.google.com/drive/folders/1VBb7OaF8CAOrwuNL413pnNYDwv-MoJoo>`__.
#. Export the image in PNG format.
#. Use a descriptive, lower-case filename, with underscores between words. Append "_es" to the filename if the content is in Spanish.
#. Store the exported version in the ``docs/_static/png`` directory in the standard's repository. Create a sub-directory to group related images, as needed, rather than using a common prefix to the filename.
