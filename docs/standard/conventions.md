# Schema conventions

This page documents conventions that MUST or SHOULD be applied when authoring OCDS schema or extensions.

## Naming conventions

See the [schema style guide](../../meta/style_guide) for guidance on naming fields.

## Definitions section

The top level of the schema is split between `properties` and `definitions`. The latter contains objects that may be re-used, by reference, in multiple locations across the schema. Each of these can be thought of as a 'Class', and its name is capitalized accordingly. Whenever you consider that an object or structure might be re-used in a different area of the standard, it should be included in `definitions`.

## ID fields

Any object that is contained within an array MUST have an `id` field. 

This is because:

* `id` values play a [special role in the flatten-tool](http://flatten-tool.readthedocs.io/en/latest/unflatten/#relationships-using-identifiers) used to round-trip between JSON and tabular representations of OCDS.
* `id` values are used to determine [how lists of objects are merged](http://standard.open-contracting.org/latest/en/schema/merging/#identifier-merge) when creating a compiledRelease.

Objects that are not contained within an array MAY include an `id` field in order to support cross-referencing, or whether the `id` relates to an identifier of the object in the real world. 

## Types and null

Any non-required field pointing to a literal, an array of literals, or an object should support a type of `null`, e.g.:

```json
{ 
  "status": {
    "title": "Contract status",
    "type": [
      "string",
      "null"
    ]
  }
}
```

Allowing properties to be `null` is important to the [merging process](http://standard.open-contracting.org/latest/en/schema/merging/), in which `null` is used to [remove a value from the compiledRelease](http://standard.open-contracting.org/latest/en/schema/reference/#emptying-fields-and-values).

Any non-required field pointing to an array of objects should not allow `null` as a value, as array entries should be explicitly tagged for removal following the pattern outlined in [standard#232](https://github.com/open-contracting/standard/issues/232).

## Detail fields

We have adopted a common pattern in OCDS of pairing a codelist with a `xDetails` field which can be used for either:

* Free text details on the codelist value
* A more detailed set of classifications from a publisher's systems

Use of `xDetails` fields can help increase acceptance of a closed codelist.

For example, a jurisdiction may have five procurement procedures, named A, B, C, D and E. The `procurementMethod` field uses a closed codelist ('open', 'selective', 'limited', 'direct') to which its procedures should be mapped. The `procurementMethodDetails` field then allows the jurisdiction to publish the original names of its procedures.

## Additional array

The `additionalX` pattern is used when:

* A data owner might have one or more values for a field
* One of those values can be considered in some way 'primary'
* A number of use cases can be met by looking only at the primary value

For example, a source system might record the company registration number and VAT identifier of a company. If we had a single `parties.identifier` object, the data owner would have to pick which identifier to use, and would be omitting data that could help some users to identify an organization. If we only had an array of `parties.identifiers`, then the data structure for the simple case (only one identifier) becomes more complex, and it is not possible to indicate any priority between the identifiers. 

Using the `additionalX` pattern, we have a field (e.g. `property`) referencing an object, paired with an `additionalProperties` field that points to an array of the same object. 
