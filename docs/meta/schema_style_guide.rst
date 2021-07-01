Schema style guide
==================

Normative statements
--------------------

.. note::
   The current version of the OCDS schema and documentation (1.1.3) does not comply with these recommendations.

-  Normative statements should be constructed using the keywords defined in `RFC2119 <https://tools.ietf.org/html/rfc2119>`__.
-  Normative keywords should be capitalized where used, per `RFC8174 <https://tools.ietf.org/html/rfc8174>`__.
-  Non-normative statements should not use the keywords defined in RFC2119, see this `Internet-Draft <https://tools.ietf.org/html/draft-hansen-nonkeywords-non2119-04>`__ for appropriate synonyms.
-  Normative statements should not use constructions such as "should always", "should only" or "where possible … must". The appropriate normative keyword should be used instead, e.g. MUST in place of "should always".
-  Normative statements must be consistent with the OCDS schema, e.g. ``ocid`` is a required field in the schema so:

   -  "the ``ocid`` field MUST be provided" is consistent.
   -  "the ``ocid`` field SHOULD be provided" is inconsistent.

-  When referring to extensions it is not necessary to explicitly state that they are optional.

Schema structure
----------------

Definitions
~~~~~~~~~~~

The top level of the schema is split between ``properties`` and ``definitions``. The latter contains objects that may be re-used, by reference, in multiple locations across the schema. Each of these can be thought of as a "Class", and its name is capitalized accordingly. Whenever you consider that an object or structure might be re-used in a different area of the standard, it should be included in ``definitions``.

Building blocks
~~~~~~~~~~~~~~~

-  The ``period`` object should be used in place of ``year`` or ``month`` fields.
-  The ``identifier`` object should be used when referencing identifiers from external sources, e.g. ``{"id": "12345678", "scheme": "IBAN"}`` rather than ``"ibanID": "12345678"``.

ID field
~~~~~~~~

Objects that are not contained within an array can include an ``id`` field to support cross-referencing, or to disclose the object's real-world identifier.

When creating a compiled release, arrays of objects have `different merging behaviors <https://standard.open-contracting.org/latest/en/schema/merging/#array-values>`__ depending on whether the schema specifies an ``id`` field. To decide whether to specify an ``id`` field:

-  If no ``id`` field is specified, the array is merged as a whole. This is appropriate if:

   -  A publisher is expected to publish array entries at the same time, like ``additionalClassifications``.
   -  A publisher is expected to correct the array as a whole.
   -  The array's semantics are release-specific, in which case the schema should also set ``"omitWhenMerged": true``.

-  If an ``id`` field is specified, the array is merged by identifier – unless the schema sets ``"wholeListMerge": true``. This is appropriate if:

   -  A publisher is expected to publish array entries at different times, like ``contracts``.

.. note::

   ``id`` values also play a `special role in Flatten Tool <https://flatten-tool.readthedocs.io/en/latest/unflatten/#relationships-using-identifiers>`__.

Details field
~~~~~~~~~~~~~

A codelist field can be paired with a ``xDetails`` string field, which can be used for:

-  Free text details on the codelist value
-  A more detailed set of classifications from a publisher's systems

Use of ``xDetails`` fields can help increase acceptance of a closed codelist.

For example, a jurisdiction may have five procurement procedures, named A, B, C, D and E. The ``procurementMethod`` field uses a closed codelist ('open', 'selective', 'limited', 'direct') to which its procedures should be mapped. The ``procurementMethodDetails`` field then allows the jurisdiction to publish the original names of its procedures.

Entered field
~~~~~~~~~~~~~

A field can be paired with a ``xEntered`` field, which can be used when some values for the field:

- Are manually entered in the data source
- Have known quality issues

An ``xEntered`` field indicates that 'this is the value entered, but we know there is a quality issue with it, and we want to spare you the trouble of addressing that quality issue'.

For example, a data source might allow users to choose the register from which an organization identifier is drawn using a dropdown, or to manually enter the name of the register if it is not in the list. Since the manual entries are non-standardized, one option is to use ``scheme`` for dropdown entries and ``schemeEntered`` for manual entries. This separates data with a known issue, and makes a (narrow) semantic distinction. 

Additional array
~~~~~~~~~~~~~~~~

An object field can be paired with a ``additionalX`` array field, which can be used when:

-  A data owner has one or more values for a field
-  One of those values can be considered in some way 'primary'
-  A number of use cases can be met by looking only at the primary value

For example, a source system might record the company registration number and VAT identifier of a company. If we had a single ``parties.identifier`` object, the data owner would have to pick which identifier to use, and would be omitting data that could help some users to identify an organization. If we only had an array of ``parties.identifiers``, then the data structure for the simple case (only one identifier) becomes more complex, and it is not possible to indicate any priority between the identifiers.

Validation keywords
-------------------

-  Date fields must use ``"format": "date-time"``.
-  URL fields must use ``"format": "uri"``.
-  Number fields should use ``minimum``, ``maximum`` and/or ``exclusiveMinimum``, if appropriate.
-  The ``default`` keyword shouldn't be used, because consumers aren't expected to fill in defaults.
-  The following keywords aren't used and might require code changes: ``additionalItems``, ``additionalProperties``, ``dependencies``, ``exclusiveMaximum``, ``maxItems``, ``maxLength``, ``maxProperties``, ``multipleOf``, ``allOf``, ``anyOf``, ``not``.

The following keywords are added by `ocdskit schema-strict <https://ocdskit.readthedocs.io/en/latest/cli/schema.html#schema-strict>`__:

-  Array fields should set ``"uniqueItems": true``.
-  Required array fields must use ``"minItems": 1``.
-  Required object fields must use ``"minProperties": 1``.
-  Required string fields must use ``"minLength": 1``, unless ``enum``, ``format`` or ``pattern`` is used.

Types and null
~~~~~~~~~~~~~~

Any non-required field pointing to a literal or an array of literals should support a type of ``null``, e.g.:

.. code-block:: json

   { 
     "status": {
       "title": "Contract status",
       "type": [
         "string",
         "null"
       ]
     }
   }

Allowing properties to be ``null`` is important to the `merging process <https://standard.open-contracting.org/latest/en/schema/merging/>`__, in which ``null`` is used to `remove a value from the compiled release <https://standard.open-contracting.org/latest/en/schema/reference/#emptying-fields-and-values>`__.

Any non-required field pointing to an array of objects should not allow ``null`` as a value; array entries should be explicitly tagged for removal following the pattern outlined in `#232 <https://github.com/open-contracting/standard/issues/232>`__.

Field and code names
--------------------

-  Check `other standards <https://lov.linkeddata.es/dataset/lov>`__ for preferred terms.
-  Use lower `camelCase <https://en.wikipedia.org/wiki/Camel_case>`__ for field names, e.g. ``awardCriteriaDetails``.
-  Use upper `CamelCase <https://en.wikipedia.org/wiki/Camel_case>`__ for ``definitions`` entries, e.g. ``Award``.
-  Put the qualifier *before* the concept, e.g. ``enquiryPeriod`` rather than ``periodOfEnquiry``.

   .. note::

      Date fields might appear inconsistent: there's ``startDate``, ``endDate``, ``maxExtentDate``, ``dueDate`` but also ``datePublished``, ``dateSigned``, ``dateModified``, ``dateMet``. The reasons are:

      -  External consistency, e.g. Schema.org uses `startDate <https://schema.org/startDate>`__, `endDate <https://schema.org/endDate>`__ but also `datePublished <https://schema.org/datePublished>`__, `dateModified <https://schema.org/dateModified>`__.
      -  Internal consistency, e.g. the fields of the ``Period`` object follow the ``*Date`` pattern.
      -  Term frequency, e.g. "due date" occurs more frequently in English than "date due".

-  Don't abbreviate words, e.g. ``minimumParticipants`` not ``minParticipants``.
-  Use singular for fields pointing to an object or literal value.
-  Use plural for fields pointing to an array of values.
-  Field names should not include their parent's name, e.g. ``title`` not ``tenderTitle``, ``description`` not ``awardDescription``, etc.

.. note::
   Many terms from OCDS 1.0 were poorly chosen; however, they can't be renamed until OCDS 2.0. For example, the semantics of the ``tender`` object are "first stage," with many publishers using that object to invite requests to participate.

   Until OCDS 2.0, publishers must use the ``tender`` term, and not choose their own terms, in order to maintain interoperability. The choice of a term is cosmetic; it's not semantic. A field's description, not its name, is semantic.

Field and code descriptions
---------------------------

-  The first sentence of a description should be descriptive of the field and written in a neutral voice, rather than addressing a particular audience. The first sentence of a description must be distinct between fields. For example, for ``tender/submissionMethod``:

   -  "The methods by which bids are submitted, using the open submissionMethod codelist." uses a neutral voice.
   -  "Specify the method(s) by which bids can be submitted" addresses publishers rather than users.

-  Subsequent sentences may provide information or guidance to assist publishers to use the field effectively or users to interpret the field effectively. Guidance sentences should be grounded in clear user needs and implementation experience of common pitfalls or errors.
-  Descriptions for similar fields or codes should be consistent with each other where possible, without discarding information relevant to a specific field.
-  For fields or codes whose names and titles use complex or specialist language, consider providing an example to aid non-expert users, e.g.

================= ===================================================== ===========
code              title                                                 Description
================= ===================================================== ===========
guaranteeReports  Fiscal commitments and contingent liabilities reports Reports detailing the fiscal commitments of the public authority to the PPP, for example known payments that must be made if the PPP proceeds or payment commitments whose occurrence, timing and magnitude depend on some uncertain future event, outside the control of the public authority.
================= ===================================================== ===========

Descriptions should:

-  Balance the needs of expert users, for whom the description serves to assure that use of the field or code is appropriate, and non-expert users, for whom the description of the code serves to help them understand how the field or code is used and whether it is likely to contain the information they are looking for.
-  Be concise and avoid using exhaustive lists.

Descriptions should **not**:

-  Link to definitions provided on external websites.
-  Explicitly state whether a field is required or optional.
-  Simply restate the title or name of a field or code.

The following examples can be used to inform descriptions for common types of fields in the schema. Additional information, specific to a particular field, should be provided in a separate sentence after the primary description of the field.

Codelists
~~~~~~~~~

.. code-block:: none

   <semantics>, using the <name> codelist. See also the <xDetails> field.

**Example:**

   The methods by which bids are submitted, using the open `submissionMethod <https://standard.open-contracting.org/%7B%7Bversion%7D%7D/%7B%7Blang%7D%7D/schema/codelists/#submission-method>`__ codelist. See also the submissionMethodDetails field.

Identifiers
~~~~~~~~~~~

For the ``id`` field of items in arrays:

.. code-block:: none

   A locally unique identifier for this <object_name>. Used to track changes to this <object_name> and to [merge](https://standard.open-contracting.org/latest/en/schema/merging/#merging) multiple releases to create a record.

**Example:**

   A locally unique identifier for this document. Used to track changes to this document and to `merge <https://standard.open-contracting.org/latest/en/schema/merging/#merging>`__ multiple releases to create a record.

Titles
~~~~~~

For the ``title`` field of an object:

.. code-block:: none

   A title for this <object_name>.

Descriptions
~~~~~~~~~~~~

For the ``description`` field of an object:

.. code-block:: none

   A description of this <object_name>. Structured information should be provided in <related_fields>.

**Examples:**

   A description of this tender. Structured information should be provided in the items array. Descriptions should be short and easy to read. Avoid using ALL CAPS.

..

   A description of this document. Descriptions should not exceed 250 words. In the event the document is not accessible online, the description field may be used to describe arrangements for obtaining a copy of the document.

Documents
~~~~~~~~~

For the ``documents`` field of an object:

.. code-block:: none

   All documents and attachments related to this <object_name>, including any official notices.

Milestones
~~~~~~~~~~

For the ``milestones`` field of an object:

.. code-block:: none

   A list of important dates or events associated with this <object_name>.
