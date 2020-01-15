# Standard

The Open Contracting Data Standard includes a **technical specification** made up of:

* An extended JSON Schema that defines objects and fields for describing a contracting process
* A set of codelists that define standard values for several fields
* A set of rules for constructing identifiers for contracting processes and organizations
* A set of rules for merging individual 'releases' into a consolidated 'record' of a contracting process
* A set of rules for transforming between JSON and tabular serializations
* An extension mechanism for describing additional fields

This section describes the processes for maintaining these assets. See the [Normative and non-normative policy](https://docs.google.com/document/d/1xjlAneqgewZvHh6_hwuQ98hbjxRcA2IUqOTJiNGcOf8/edit) for details on which sections of the documentation are normative or not.

Documentation is written in Markdown syntax with [recommonmark](https://recommonmark.readthedocs.org/en/latest/) building on [Commonmark](http://commonmark.org/).

```eval_rst
.. toctree::
   :maxdepth: 2
   :glob:

   schema
   conventions
   translation/index
   technical/index
```

## Reading list

To get up to speed on OCDS standard development, you should be familiar with:

* The standard itself
  * [OCDS documentation](https://standard.open-contracting.org/), in particular the schema and codelists
  * [Extension Explorer](https://extensions.open-contracting.org/)
* The policies it follows
  * [Normative and non-normative content and changes policy](https://docs.google.com/document/d/1xjlAneqgewZvHh6_hwuQ98hbjxRcA2IUqOTJiNGcOf8/edit)
  * [Translation and localization policy](https://standard.open-contracting.org/1.1/en/support/governance/#translation-and-localization-policy)
  * [Extension classification policy](https://docs.google.com/document/d/1zvR1PDefO6yTK28uKA6XCnxMLiC9oiEeb3uFjHuRyqI/edit) (draft)
  * [Semantic versioning](https://semver.org)

For practical information on standard development, read this section and:

* Other sections of this handbook:
  * [Meta](../../meta)
  * [Extensions](../../extensions)
  * [Profiles](../../profiles)
* The [Schema patterns](https://os4d.opendataservices.coop/patterns/schema/) section of [ODS' Standards Lab](http://os4d.opendataservices.coop/)

We strive to write concise, clear documentation. To improve your writing, please learn how to [write for the web](https://www.usa.gov/style-guide/writing-for-web) (with many more resources at [Nielsen Norman Group](https://www.nngroup.com/topic/writing-web/)), and consider using these tools:

* [Hemingway Editor](http://www.hemingwayapp.com/)
* [Grammarly](https://www.grammarly.com/)
* Readability statistics in Microsoft Word or [online tools](https://www.webfx.com/tools/read-able/flesch-kincaid.html)

For the history of standard development, read:

* [2018 OCDS objectives and design decisions](https://docs.google.com/document/d/1j6Ec1vV0DklKMYvIBpeoIjABXDRT0nFythGNJR2ms24/edit)
* [2018 Extension mechanism design decisions](https://docs.google.com/document/d/1zV0_UeVTGEdLRq5DQEH3XAUWl0HrHNNQPEwftLkHqBQ/edit)
* [2018 Extension registry design decisions](https://docs.google.com/document/d/18JLz_RqBkYiDE-HSlzoa9_2XxgxYUmV9O2VnbMfc_Ss/edit)
* [2018 Short history of standard development](https://docs.google.com/document/d/118NBDV6YIxlk75vc_8nmV0_GmacsQjes7xBXzoNSiY0/edit)
* The [Development](https://os4d.opendataservices.coop/development/) section of ODS' Standards Lab
* [2014 technical scoping](https://github.com/open-contracting-archive/technical-approach/blob/master/README.md)

The [standard](https://github.com/open-contracting/standard/issues) and [ocds-extensions](https://github.com/open-contracting/ocds-extensions/issues) repositories contain all public discussions about standard development.
