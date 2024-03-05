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

-  Always **package data** in a release or record package.
-  Use **real examples**: that is, examples that feature real organizations and plausible and coherent field values. Generic examples are much less compelling and clear to readers, for a variety of reasons:

   -  There's a tendency for generic data to become overly generic: for example, Anytown procures Thingamajigs for the greater benefit of the Republic of Atlantis.
   -  Fictional entities aren't immediately recognized by readers, unlike London, IBM, etc.
   -  Specific examples tend to be more memorable and interesting than generic ones.
   -  Readers have to think more when given a generic/abstract example than a specific/concrete one.
   -  Real examples better ensure that the example makes sense. When you have the Fisheries Department procuring oil pipelines, you think “Well, hold on a minute” and then fix it to be more realistic. When data is generic and ambiguous, it's easy to let unclear scenarios through.
   -  Specific examples can communicate facts by implication. If the example is about cross-border procurement, you can pick a real buyer and supplier that are well-known to be based in different countries. You would still include their countries, but readers won't need that to understand.

-  Avoid using real data from publishers. It is rarely worth the effort to find suitable data, correct any errors and trim it down for brevity and clarity.
-  Keep examples simple, and omit irrelevant fields. For example, to illustrate an amendment, change a single field's value, and omit optional fields with unchanged values.
-  Examples on the same page ought to follow a common thread, context or scenario, so that readers don't need to reorient themselves to each example.

Guidelines in practice
~~~~~~~~~~~~~~~~~~~~~~

The [tender updates and amendments example](https://standard.open-contracting.org/1.1/en/guidance/map/amendments/#example-1-tender-updates-and-amendments) in OCDS 1.1 has the following issues:

* Overly generic: The buyer (Open Data Services) is not a government agency and appears elsewhere in the documentation as a supplier. The object of the procurement (a data merging tool) closely relates to the subject of the example (updates and amendments), which is confusing.
* Irrelevant fields: Many fields are irrelevant to the subject – like `tender.status`, `tender.procurementMethod` and `tender.awardPeriod`. Readers need to scan more JSON to find relevant lines.
* The [tender amendment release](https://standard.open-contracting.org/1.1/en/guidance/map/amendments/#tender-amendment) is unnecessarily complex: it amends two fields (`tender.value` and `tender.period`), when one is sufficient to illustrate how amendments are modeled.

OCDS 1.2 [simplifies the example](https://standard.open-contracting.org/staging/1666-make-examples-minimal/en/guidance/map/amendments/#example-1-tender-updates-and-amendments) to meet the guidelines.
