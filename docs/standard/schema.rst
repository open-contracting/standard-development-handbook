The schema
==========

``release-schema.json`` is the Single Source of Truth (SSOT) for defining OCDS’ objects and fields. It is documented using an extended version of `JSON Schema draft 4 <https://tools.ietf.org/html/draft-zyp-json-schema-04>`__ (see below).

The source for ``release-schema.json`` and other schema files is in the ```standard`` repository <https://github.com/open-contracting/standard>`__ in the `schema directory <https://github.com/open-contracting/standard/tree/HEAD/schema>`__.

These schema files are processed during the `documentation build <technical/build>`__ and `deployment process <technical/deployment>`__ to replace ``{lang}`` and ``{version}`` tokens.

Forward and backwards compatibility
-----------------------------------

The standard’s documentation contains a `deprecation policy <https://standard.open-contracting.org/latest/en/schema/deprecation/>`__ and a description of its approach to `semantic versioning <https://standard.open-contracting.org/latest/en/support/governance/#versions>`__.

Our extensions to JSON Schema
-----------------------------

We add to JSON Schema the properties ``codelist``, ``openCodelist``, ``deprecated``, ``omitWhenMerged`` and ``wholeListMerge``, documented in the `Open Standards for Data <https://os4d.opendataservices.coop/development/schema/#extended-json-schema>`__ handbook and defined in a `metaschema patch <https://github.com/open-contracting/standard/tree/HEAD/schema/metaschema>`__.
