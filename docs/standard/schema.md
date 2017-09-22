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

All issues should be closed with a brief rationale. This comment makes it easy to understand what happened and affords participants an opportunity to engage with the rationale. Examples of simple rationales are:

* "Resolved in the above commit" if there's a commit referencing the issue that appears nearby
* "Resolved in the [name] extension" with a link to the extension that was created
* "Closing, because [explanation]"

Some issues produce long discussions, and the original intent of the issue may change over time; this can make it more difficult to catch up on the current state of the issue. To deal with this, rather than closing the issue and opening a fresh issue, the issue's description should be edited to reflect the current state of the issue, summarize the discussion so far, and link to the most recent comment from which the discussion may continue.

Restarting the discussion with a new issue causes the following problems:

* Old participants aren't notified of activity on the new issue, and need to diligently subscribe to it.
* New participants need to diligently read all issues referencing the new issue to rebuild the context.
* If the old issue is closed in favor of a new issue, and the new issue is thereafter not resolved but is closed (for whatever reason, like insufficient demand), a reader of the old issue may assume that the new issue is either open or resolved. They would need to follow the chain to realize that it's unresolved and closed, before adding a comment to say, "I need this."

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
