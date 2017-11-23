# Schema conventions

This page documents conventions that MUST or SHOULD be applied when authoring OCDS schema or extensions.

## Definitions section

The top level of the schema is split between `properties` (the basic structure of an OCDS release) and `definitions` (containing objects that may be re-used in multiple locations across the schema) which are referenced whenever they are used. 

Each of the objects in `definitions` can be thought of as a 'Class', and it's name is capitalised accordingly. 
 
Whenever you consider that an object or structure might be re-used in a different area of the standard, it should be included in `definitions`, and referenced. 

## Naming conventions

We use lower [camelCase](https://en.wikipedia.org/wiki/Camel_case) for property names. E.g. `awardCriteriaDetails`.

We use upper [CamelCase](https://en.wikipedia.org/wiki/Camel_case) for objects directly nested within in the `definitions` section. E.g. `Award`.

We put the qualifier *before* the concept. E.g. `enquiryPeriod` rather than `periodOfEnquiry`.

We use singular for properties pointing to an object or literal value.

We use plural for properties pointing to an array of values. 


## ID fields

Any object that is contained within an array MUST have an `id` field. 

This is because:

* `id` values play a [special role in the flatten-tool](http://flatten-tool.readthedocs.io/en/latest/unflatten/#relationships-using-identifiers) used to round-trip between JSON and tabular representations of OCDS;
* `id` values are used to determine [how lists of objects are merged](http://standard.open-contracting.org/latest/en/schema/merging/#identifier-merge) when creating a compiledRelease. 

Objects that are not contained within an array MAY include an `id` property in order to support cross-referencing, or whether the `id` relates to an identifier of the object in the real world. 

## Types and null

Any non-required property pointing to a literal, array of literals, or single object should support a type of `null`. E.g.:

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

(To be confirmed:) Any non-required property pointing to an array of objects should not allow `null` as a value, as array entries should be explicitly tagged for removal following the pattern outlined in [Standard#232](https://github.com/open-contracting/standard/issues/232) 

```eval_rst
  .. todo::
    Confirm the guidance on null above. :issue:`75`
```

## Detail fields

We have adopted a common pattern in OCDS of pairing a codelist, with a `Details` field which can be used for either:

* Free text details on the codelist value;
* A more detailed set of classifications from a publisher's systems;

For example, a country may have five procurement procedures: A, B, C, D and E. 

The `procurementMethod` field uses a closed codelist ('open','selective','limited','direct') to which these five procedures should be mapped. The `procurementMethodDetails` field then exists, into which they can input their original, unmapped classifications: A, B, C, D or E. 

Use of `Detail` fields can help increase acceptance of a closed codelist.

## Additional array

The `additionalX` pattern is used when:

* A data owner might have one or more values for a property;
* One of those values can be considered in some way 'primary';
* A number of use-cases can be met by looking only at the primary value.

For example, a source system may record the company registration number and VAT identifier of a company. If we had a single `parties.identifier` object, the data owner would have to pick which identifier to use, and would be omitting data that could help some users to identify an organisation. If we only had an array of `parties.identifiers`, then the data structure for the simple case (only one identifier) becomes more complex, and it is not possible to indicate any priority between the identifiers. 

Using the `additionalX` pattern we have a property (e.g. `property`) referencing an object, paired with an `additionalProperties` property that points to an array of the same object. 


