# The schema

`release-schema.json` is the Single Source of Truth (SSOT) for defining OCDS' fields and data structures. It is documented using an extended version of [JSON Schema draft 4](https://tools.ietf.org/html/draft-zyp-json-schema-04) (see below).

The source for `release-schema.json` and other schema files is in the [`standard` repository](https://github.com/open-contracting/standard) in the [standard/standard/schema directory](https://github.com/open-contracting/standard/tree/HEAD/standard/schema).

These schema files are processed during the documentation build and deployment process to replace `{lang}` and `{version}` tokens. Each Travis build of the documentation checks whether `versioned-release-validation-schema.json` is up-to-date.

```eval_rst
  .. todo::
    Add a link or a new page for describing the build and deployment process.
```

## Issue tracking

```eval_rst
  .. todo::
    Document how issues requesting updates to the standard should be handled.
```

## Forward and backwards compatibility

A conformance statement in the standard's documentation provides guidance on how forward and backwards compatibility should be interpreted.

```eval_rst
  .. todo::
    We need to further develop the conformance statement to capture all forward and backwards compatibility scenarios.
```

## Our extensions to JSON Schema

```eval_rst
  .. todo::
    Document the additional properties we added to JSON Schema.
```
