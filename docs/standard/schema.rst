The schema
==========

``release-schema.json`` is the Single Source of Truth (SSOT) for defining OCDS' objects and fields. It is documented using an extended version of `JSON Schema draft 4 <https://tools.ietf.org/html/draft-zyp-json-schema-04>`__ (see below).

The source for ``release-schema.json`` and other schema files is in the `standard repository <https://github.com/open-contracting/standard>`__ in the `schema directory <https://github.com/open-contracting/standard/tree/HEAD/schema>`__.

These schema files are processed while :doc:`technical/build` and during :doc:`technical/deployment` to replace ``{lang}`` and ``{version}`` tokens.

Forward and backwards compatibility
-----------------------------------

The standard's documentation contains a `deprecation policy <https://standard.open-contracting.org/latest/en/schema/deprecation/>`__ and a description of its approach to `semantic versioning <https://standard.open-contracting.org/latest/en/support/governance/#versions>`__.

Our extensions to JSON Schema
-----------------------------

We add to JSON Schema the properties ``codelist``, ``openCodelist``, ``deprecated``, ``omitWhenMerged`` and ``wholeListMerge``, documented in `Standards Lab <https://os4d.opendataservices.coop/development/schema/#extended-json-schema>`__ and defined in a `metaschema patch <https://github.com/open-contracting/standard/tree/HEAD/schema/metaschema>`__.

.. seealso::

   `Open Data Services JSON Schema Extension <https://json-schema-extension.readthedocs.io/latest/>`__
