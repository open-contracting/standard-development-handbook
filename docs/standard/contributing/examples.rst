Add an example
==============

Providing examples helps users to understand how certain concepts or processes are modelled in OCDS.

Examples are typically composed of sample OCDS JSON data and a narrative description of the concepts or processes modelled in the data.

This document describes the process for drafting and producing a single example, and describes guidelines for producing sample OCDS JSON data.

Process
-------

#. Check for relevant open issues in the `standard repository <https://github.com/open-contracting/standard/issues>`__ and, if relevant, `ocds-extensions <https://github.com/open-contracting/ocds-extensions/issues>`__ repository. New issues might have been created since the example was discussed.

#. Create a GitHub issue in the ``standard`` repository about adding the example.

#. Create a document in the `Examples folder <https://drive.google.com/drive/folders/1gx7UU1xdVshOiBUXFupnOb7GSzuEpPVW>`__ and outline the:

   -  scope of the example
   -  key concepts covered
   -  structure of the example
   -  any sample JSON files (or extracts) that will be produced

#. Agree the outline for the example, by sharing the document in the GitHub issue. If the example is relevant to any specific OCP engagements, inform the relevant program managers on Slack.

#. Draft the example, taking note of the :ref:`examples-guidelines`

   #. Draft the narrative in the document.

   #. Draft the sample data. There are different approaches to authoring sample data, for example:

      -  Start from the `blank JSON template <https://github.com/open-contracting/sample-data/tree/master/blank-template>`__
      -  Start from a spreadsheet (e.g. when the example includes multiple releases)

      Put the sample data in `GitHub Gist <https://gist.github.com/>`__ or in a subfolder of the `Examples folder <https://drive.google.com/drive/folders/1gx7UU1xdVshOiBUXFupnOb7GSzuEpPVW>`__, and link to it from the document.

#. Update the GitHub issue and solicit a first review, then address any feedback
#. Update the GitHub issue and solicit a final review from  James, then address any feedback
#. Create a branch on the `standard repository <https://github.com/open-contracting/standard>`__ and add:

   -  A Markdown file containing the narrative
   -  JSON files containing the sample data, following the :ref:`convention<json-example-filenames>`

   Use the `jsoninclude <https://sphinxcontrib-opendataservices.readthedocs.io/en/latest/jsoninclude/>`__ directive to include excerpts from the sample data in the narrative.

#. Create a pull request to merge the example, following the :doc:`usual process<../contributing>`.

.. _examples-guidelines:

Guidelines
----------

-  Always package data in a release or record package.
-  Use real examples. That is, examples that feature real organizations and plausible and coherent field values. Generic examples are much less compelling and clear to readers, for a variety of reasons: 

   -  There’s a tendency for generic data to become overly generic, e.g. Anytown procures Thingamajigs for the greater benefit of the Republic of Atlantis.
   -  Fictional entities aren’t immediately recognized by readers, unlike London, IBM, etc.
   -  Specific examples tend to be more memorable and interesting than general ones.
   -  Readers have to think more when given a generic/abstract example than a specific/concrete one.
   -  Real examples better ensure that the example makes sense. When you have the Fisheries Department procuring oil pipelines, you think “Well, hold on a minute” and then fix it to be more realistic. When data is generic and ambiguous, it’s easy to let unclear scenarios through.
   -  Specific examples help to communicate facts by implication. If the example is about cross-border procurement, you can pick a real buyer and supplier that are well-known to be based in different countries. You would include their different countries in the data, but readers won’t have to see that to understand.

-  Avoid using real data from OCDS publishers. It is rarely worth the effort of finding suitable data, correcting errors and trimming it down for brevity and clarity.
-  Keep examples as simple as possible and omit fields that aren't relevant to the example. For example, to illustrate an amendment, amend the value of a single field and omit optional fields with unchanged values.
-  Examples on the same page ought to follow a common thread/context/scenario so that readers do not need to reorient themselves to each example.

Guidelines in practice
~~~~~~~~~~~~~~~~~~~~~~

The [tender updates and amendments example](https://standard.open-contracting.org/1.1/en/guidance/map/amendments/#example-1-tender-updates-and-amendments) in OCDS 1.1 has the following deficiencies:

* The example is overly generic: the buyer (Open Data Services) is not a government agency and appears elsewhere in the documentation as a supplier and the object of the procurement (a data merging tool) closely relates to the subject of the example (updates and amendments), which is confusing for readers.
* The example data contain many fields that are irrelevant to the subject of the example, e.g. `tender.status`, `tender.procurementMethod` and `tender.awardPeriod`, which means readers need to scan lots of JSON to find the important parts.
* The [tender amendment release](https://standard.open-contracting.org/1.1/en/guidance/map/amendments/#tender-amendment) is unnecessarily complex: it amends two fields (`tender.value` and `tender.period`), when only one is needed to illustrate how amendments are modelled, which is confusing for readers.

OCDS 1.2 features a simplified version of the example that conforms to the above guidelines.
