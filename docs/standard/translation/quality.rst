Quality assurance
=================

During translation, use the :ref:`glossary` and follow the :ref:`translation-style-guide`, below.

After translation, `translate-toolkit <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/installation.html>`__ offers many `quality assurance <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/index.html#commands-quality-assurance>`__ tools. You can:

-  `Check for common errors <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/guides/using_pofilter.html>`__ with `pofilter <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/pofilter.html>`__, as described below
-  `Check for inconsistencies in your translations <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/guides/checking_for_inconsistencies.html>`__ with `poconflicts <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/poconflicts.html>`__

.. _glossary:

Glossary
--------

We ensure that key terms are translated consistently using a `Transifex glossary <https://help.transifex.com/en/articles/6229127-understanding-glossaries>`__: for example, the `OCDS glossary <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/glossary/es/>`__.

Manage the glossary
~~~~~~~~~~~~~~~~~~~

The Coordinator works with Translators to `update <https://docs.google.com/spreadsheets/d/171VRailLhqC3Pmw3Qkh4lIgUkmtSa7t4H2h7yntSZg8/edit#gid=0>`__ the glossary in Google Sheets. Then, the Coordinator `uploads <https://help.transifex.com/en/articles/6229147-adding-terms-to-a-glossary#h_a2652dd8c0>`__ the glossary to Transifex.

.. note::

   Use `poterminology <https://docs.translatehouse.org/projects/translate-toolkit/en/latest/commands/poterminology.html>`__ to identify potential new terms.

Use the glossary
~~~~~~~~~~~~~~~~

Translators review and correct translations with :ref:`warnings<view-translations-with-warnings>`.

.. seealso::

    `Using the Glossary <https://help.transifex.com/en/articles/6240837-using-the-glossary>`__

.. _translation-style-guide:

Translation style guide
-----------------------

Please read the :doc:`general style guides<../../meta/index>` for context.

Markdown format
~~~~~~~~~~~~~~~

Do not change the whitespace around Markdown text. For example, do not change ``**Action:**`` to ``** Acción: **``. In particular, do not add spaces between the brackets and parentheses in a Markdown link (``[some text](url)``).

Punctuation
~~~~~~~~~~~

Please double-check that the ending punctuation is the same. A common error is to omit a final period.

Quoted words
~~~~~~~~~~~~

Words in backticks (like ``tender``) or in single quotation marks (like 'direct') are typically the names of fields or codes and must not be translated.

URLs
~~~~

You may change the URL to an equivalent in that language, if available. For example, the OC4IDS documentation links to the OCDS documentation. Change the language path component in OCDS documentation URLs, e.g. ``https://standard.open-contracting.org/latest/en/guidance/`` to ``https://standard.open-contracting.org/latest/es/guidance/``.

Gender
~~~~~~

If the text to translate is, for example, an adjective that isn't accompanied by a noun, determine the gender to apply by checking the context in which the word is used (e.g. open in the corresponding documentation page in English).

Tone
~~~~

Prefer the formal "usted" over the informal "tu". For example, "Understand your context" is translated as "Entienda su contexto".

Proper nouns and acronyms
~~~~~~~~~~~~~~~~~~~~~~~~~

Translate proper nouns and keep acronyms in English. For example, "United Nations Standard Products and Services Code (UNSPSC)" is translated as "Código de Productos y Servicios Estándar de las Naciones Unidas (UNSPSC, en inglés)".

Changelog entries
~~~~~~~~~~~~~~~~~

Translate the initial verbs as their infinitive form, e.g. “add” to "agregar", “make” to "hacer", “remove” to "eliminar". 

.. note::

   Changelog entries are read as "This change will ...", which is equivalent to "Este cambio va a ...".

Resources
~~~~~~~~~

You can lookup translations of technical terms in:

-  `Spanish UNCITRAL glossary <https://uncitral.un.org/sites/uncitral.un.org/files/media-documents/uncitral/es/glossary-s.pdf>`__ (compare to `English <https://uncitral.un.org/sites/uncitral.un.org/files/media-documents/uncitral/en/glossary-e.pdf>`__)
-  `Procurement-related terms from Latin America <https://docs.google.com/spreadsheets/d/1DHdqfb5tvtpDOgLcuipZt1O7POCT4Jqe20-5DlGoiqw/edit#gid=1648356123>`__
-  `World Trade Organization Revised Agreement on Government Procurement <https://www.wto.org/spanish/docs_s/legal_s/rev-gpr-94_01_s.htm>`__ (compare to `English <https://www.wto.org/english/docs_e/legal_e/rev-gpr-94_01_e.htm>`__)

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
     - ``E.g.`` ``P. Ej.``, ``Examples`` ``Ejemplos Prácticos``
   * - startcaps
     - Caused by adding spaces around inline markup.
     - ``** Acción: **``
   * - sentencecount
     - Missing periods and inline markup or punctuation around periods can cause sentence counts to be incorrect.
     - ``**schema.**``, ``“records.”``
