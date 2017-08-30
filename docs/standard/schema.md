# The schema

release-schema.json is the Single Source of Truth (SSOT) for defining the fields and data structures used by the standard.

It is documented using an extended version of [JSON Schema draft 4](https://tools.ietf.org/html/draft-zyp-json-schema-04) (see below).

The source for release-schema.json lives in the [standard repository](https://github.com/open-contracting/standard) in the [standard/standard/schema folder](https://github.com/open-contracting/standard/tree/HEAD/standard/schema)

There are also schema files for release and record packages in this folder.

These schema files are processed during the documentation [build and deployment process](TODO) to replace {lang} and {version} tokens, and to generate a versioned-release-validation-schema.json file. 

```eval_rst 
  .. todo:: 
    Check that versioned-release-validation-schema.json is being auto-generated now. It may still be manually prepared at the moment. 
```

## Issue tracking

```eval_rst 
  .. todo:: 
    Document how issues requesting updates to the standard should be handled.
```

## Versioning

We use semantic versioning for the standard.

A conformance statement in the main standard documentation provides guidance on how forward and backwards compatibility should be interpreted. 

```eval_rst 
  .. todo:: 
    We need to further develop the conformance statement to capture all forward compatibility and backwards compatibility scenarios. 
```

## Issue tracking

```eval_rst 
  .. todo:: 
    Document how issues requesting updates to the standard should be handled.
```

## Our extensions to JSON Schema

```eval_rst 
  .. todo:: 
    Document the additional properties we have added to JSON schema
```