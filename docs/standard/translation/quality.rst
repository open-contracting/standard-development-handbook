Quality assurance
=================

During translation, use the :ref:`glossary`.

After translation, `translate-toolkit <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/installation.html>`__ offers many `quality assurance <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/index.html#commands-quality-assurance>`__ tools. You can:

-  `Check for common errors <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/guides/using_pofilter.html>`__ with `pofilter <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/pofilter.html>`__, as described below
-  `Check for inconsistencies in your translations <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/guides/checking_for_inconsistencies.html>`__ with `poconflicts <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/poconflicts.html>`__

.. _glossary:

Glossary
--------

We ensure that key terms are translated consistently using a `Transifex glossary <https://docs.transifex.com/glossary/glossary>`__: for example, the `OCDS glossary <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/glossary/es/>`__.

Manage the glossary
~~~~~~~~~~~~~~~~~~~

The Coordinator works with Translators to `update <https://docs.google.com/spreadsheets/d/171VRailLhqC3Pmw3Qkh4lIgUkmtSa7t4H2h7yntSZg8/edit#gid=0>`__ the glossary in Google Sheets. Then, the Coordinator `uploads <https://docs.transifex.com/glossary/uploading-an-existing-glossary>`__ the glossary to Transifex.

.. note::

   Use `poterminology <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/poterminology.html>`__ to identify potential new terms.

Use the glossary
~~~~~~~~~~~~~~~~

Translators review and correct translations with :ref:`warnings<view-translations-with-warnings>`.

.. seealso::

    `Using the Glossary <https://docs.transifex.com/translation/using-the-glossary>`__

pofilter
--------

``pofilter -l`` provides a long list of checks.

It is recommended to run one check at a time, as it is easier to fix the same type of problem all at once. Then, commit all fixes from a single check at once, to similarly make it easier to review. For example:

.. code-block:: bash

   pofilter --language=es -i es -o errors -t numbers

Read the comment that starts with ``# (pofilter)`` to understand the cause of the error. For example:

.. code-block:: none

   # (pofilter) sentencecount: Different number of sentences: 2 ≠ 3

Recommended checks
~~~~~~~~~~~~~~~~~~

This list is based on a single run of ``pofilter`` against the ``es`` locale in the standard's repository.

.. list-table::
   :header-rows: 1

   * - Filter
     - Documentation
     - Notes
   * - numbers
     - Checks whether numbers of various forms are consistent between the two strings.
     -
   * - doublewords
     - Checks for repeated words in the translation.
     -
   * - simpleplurals
     - Checks for English style plural(s) for you to review.
     - "(s)" plurals are against the :doc:`../../meta/style_guide`.
   * - brackets
     - Checks that the number of brackets in both strings match.
     - To find Markdown errors, use the regular expression ``brackets:(?! (Added|Missing) '\(', '\)'\n)``. To find other errors, remove ``|Missing`` from the regular expression. Otherwise, parentheses are often added around a machine/English term.
   * - doublequoting
     - Checks whether doublequoting is consistent between the two strings.
     - Smart quotation marks are against the :doc:`../../meta/style_guide`. Otherwise, there is likely a mismatch, e.g. a missing quote, or double quotes instead of single quotes or backticks.
   * - newlines
     - Checks whether newlines are consistent between the two strings.
     - Correct the error if the newline causes a visible change.

At time of writing, ``pofilter`` implements 46 checks, of which these 27 yield no errors:

.. code-block:: bash

   pofilter --language=es -i es -o errors -t accelerators -t blank -t compendiumconflicts -t credits -t emails -t escapes -t filepaths -t functions -t hassuggestion -t isfuzzy -t isreview -t kdecomments -t long -t musttranslatewords -t notranslatewords -t nplurals -t options -t printf -t purepunc -t pythonbraceformat -t short -t spellcheck -t tabs -t untranslated -t validchars -t variables -t xmltags

Optional checks
~~~~~~~~~~~~~~~

Some checks are very common, but not important to fix:

.. list-table::
   :header-rows: 1

   * - Filter
     - Description
     - Notes
   * - endpunc
     - Checks whether punctuation at the end of the strings match.
     - Translators frequently add or omit a period from the text's end – but this does not cause misinterpretation by readers.
   * - urls
     - Checks that URLs are not translated.
     - In most cases, the URL is translated on purpose.

       .. note::

          These errors can also be reviewed in Transifex.

False positives
~~~~~~~~~~~~~~~

Some checks are very likely to produce false positives:

.. list-table::
   :header-rows: 1

   * - Filter
     - Notes
     - Example 
   * - doublespacing
     - Authors and translators sometimes type an extra space between words. This has no visible effect.
     -
   * - endwhitespace
     - Translators sometimes type an extra space at the text's end. This has no visible effect.
     -
   * - startwhitespace
     - Translators rarely type an extra space at the text's start. This has no visible effect.
     -
   * - puncspacing
     - Moving inline markup or parentheticals next to other punctuation causes the punctuation spacing to change.
     - ``(OCDS)`` ``(OCDS),``
   * - startpunc
     - Moving inline markup to the text's start causes the first punctuation to change. Questions start with ¿ in Spanish.
     - ``**Open Data**`` ``Los **Datos Abiertos**``
   * - unchanged
     - OCDS has many words that shouldn't be translated that sometimes appear on their own.
     - ``tender``
   * - singlequoting
     - English plural possessives introduce single quotes.
     - ``OCDS'``
   * - acronyms
     - Acronyms are expected to change across languages, especially for Spanish.
     - ``WTO`` ``OMC``
   * - simplecaps
     - Caused by different choices for, or styles of, capitalization.
     - ``E.g.`` ``P. Ej.``, ``Worked examples`` ``Ejemplos Prácticos``
   * - startcaps
     - Caused by adding spaces around inline markup.
     - ``** Acción: **``
   * - sentencecount
     - Missing periods and inline markup or punctuation around periods can cause sentence counts to be incorrect.
     - ``**schema.**``, ``“records.”``
