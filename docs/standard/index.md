# Standard

```eval_rst
  .. todo::
    Identify clearly which sections of the documentation are normative and which are non-normative. :issue:`25`
```

The Open Contracting Data Standard consists of:

* **A technical specification** made up of:
  * An extended JSON Schema that defines a set of fields and data structures that can be used to describe a contracting process
  * A set of codelists that define valid or recommended values for several fields
  * A set of rules for the construction of identifiers for contracting processes and organizations
  * A set of rules for transforming between JSON and tabular serializations
  * A set of rules for merging multiple JSON 'releases' into a consolidated 'record' of a contracting process
* **Normative documentation** describing how to implement and evaluate implementation of the specification
* **Non-normative guidance** contained within the documentation
* **Guidance on publication levels** describing recommended fields and approaches to data publication
* **An extensions mechanism** for declaring additional fields not covered by the core standard

This section describes the processes for maintaining these assets.

Documentation is written in Markdown syntax with [recommonmark](https://recommonmark.readthedocs.org/en/latest/) building on [Commonmark](http://commonmark.org/).

```eval_rst
.. toctree::
   :maxdepth: 2
   :glob:

   schema
   conventions
   guidance
   translation/index
   technical/index
   *
```
