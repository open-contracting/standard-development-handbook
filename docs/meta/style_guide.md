# Style guide

This style guide covers our conventions when writing:

* OCDS Schema and standard documentation
* GitHub issues
* Helpdesk responses
* Associated presentations and documents

## Spelling

Use American English (e.g. 'organization' rather than 'organisation') unless we are aligning a field name with an existing standard that uses alternative spellings. Notably, this means being careful about using 'z' instead of 's' in many words of Latin origin.

## Text formatting

* When referring to a **field** or **codelist**, use the camelCase version of the field/codelist name, and enclose it in backticks so it is displayed in a montotype font as follows: `camelCase`
* When referring to a **building block**, use the capitalized CamelCase version of the building block name, and enclose it in backticks so it is displayed in a montotype font as follows: `CamelCase`
* When referring to a **code** from a codelist, enclose the value in single quotes, e.g. "We have added a 'direct' code to the `method` codelist"
* When pluralizing a **field** or **building block**, treat the field/building block name as a proper noun, and add a `'s` instead of an `s` to the end, or treat it as a mass noun and add nothing to the end

## Word choice

* 'ocid' not 'OCID'. Although abbreviations in prose are uppercase, the mixing of upper- and lowercase in the documentation (when referring to the concept versus the field) may cause confusion.
* 'codelist' not 'code-list' or 'code list'
* 'changelog' not 'change-log' or 'change log'
* 'data package' not 'datapackage'
* 'metadata' not 'meta-data' or 'meta data'

## Schema style guide

* We use lower [camelCase](https://en.wikipedia.org/wiki/Camel_case) for property names, e.g. `awardCriteriaDetails`.
* We use upper [CamelCase](https://en.wikipedia.org/wiki/Camel_case) for objects directly nested within the `definitions` section, e.g. `Award`.
* We put the qualifier *before* the concept, e.g. `enquiryPeriod` rather than `periodOfEnquiry`.
* We use singular for properties pointing to an object or literal value.
* We use plural for properties pointing to an array of values. 
* Property and object names should not include the name of the parent object, e.g. `title` not `tenderTitle`, `description` not `awardDescription`, etc.
* Date fields should use the `"format": "date-time"` key to enforce use of ISO8601
* The `period` object should be used in place of `year` or `month` fields
* Where a property is an object, the object should be defined in the `definitions` section of the JSON Schema and referenced with `$ref`, rather than nesting properties of properties
* The `identifier` object should be used when referencing identifiers from external sources, e.g. `{"id": "12345678", "scheme": "IBAN"}` rather than `"ibanID": "12345678"`
* For codelists, consider whether a supporting free-text `codelistDetails` field is required

## Handbook style guide

Handbook contributors should follow this style guide.

### Links

When linking to a GiHub resource, use `HEAD` instead of a specific branch, tag or commit.

When linking to the standard's documentation, use the `latest` build instead of a specific version.

### Structure

Unless a page is short, it should start with a description of its contents.

If relevant, a page should include a section on **testing** that describes the tests to verify work.

### Admonitions

Admonitions (box outs) can be added using the **hint**, **note** and **warning** styles.

```eval_rst
  .. todo::
    Use a todo admonition to indicate issues in the documentation that need to be addressed, but only if a corresponding GitHub issue exists and is linked from the documentation using the :issue:`nn` syntax.
```

```eval_rst
  .. hint::
    Use a hint admonition to share extra information that may be useful for a user of the documentation.
```

```eval_rst
  .. note::
    Use a note admonition to indicate that there are areas where the documentation requires further improvement, but this does not block use of the current information.
```

```eval_rst
  .. warning::
    Use a warning admonition to indicate that the documentation on a page may not accurately reflect current practice, or that substantial caveats exist that should be noted before following the documented process.
```

### Email addresses

If an email address is discoverable on Google, there is no use in simple obfuscations like [at] and [dot] that make the text less readable. If an email address is not yet public, it is best to keep it that way than to attempt obfuscation.
