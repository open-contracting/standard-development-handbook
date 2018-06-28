# The schema

`release-schema.json` is the Single Source of Truth (SSOT) for defining OCDS' fields and data structures. It is documented using an extended version of [JSON Schema draft 4](https://tools.ietf.org/html/draft-zyp-json-schema-04) (see below).

The source for `release-schema.json` and other schema files is in the [`standard` repository](https://github.com/open-contracting/standard) in the [standard/standard/schema directory](https://github.com/open-contracting/standard/tree/HEAD/standard/schema).

These schema files are processed during the [documentation build](../technical/build) and [deployment process](../technical/deployment) to replace `{lang}` and `{version}` tokens. Each Travis build of the documentation checks whether `versioned-release-validation-schema.json` is up-to-date.

## Forward and backwards compatibility

The standard's documentation contains a [deprecation policy](http://standard.open-contracting.org/latest/en/schema/deprecation/) and a description of its approach to [semantic versioning](http://standard.open-contracting.org/latest/en/support/governance/#versions).

```eval_rst
  .. todo::
    We need to further develop the conformance statement to capture all forward and backwards compatibility scenarios.
```

## Our extensions to JSON Schema

We use a number of additional JSON Schema properties: `codelist`, `openCodelist`, `deprecated` and a set of merge strategies properties. These are documented in the [Open Standards for Data](http://os4d.opendataservices.coop/development/schema/#extended-json-schema) handbook and are available via a [metaschema patch](https://github.com/open-contracting/standard/tree/HEAD/standard/schema/metaschema). 
