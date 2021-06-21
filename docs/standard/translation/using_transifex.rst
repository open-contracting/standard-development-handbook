Using Transifex
===============

Steps for translators, proofreaders and reviewers
-------------------------------------------------

Translator
~~~~~~~~~~

Before beginning, ask the :ref:`Coordinator<roles>` to ensure that the :ref:`Transifex glossary<glossary>` is up-to-date. If the glossary is not yet available in your language, ask the Coordinator to arrange it.

1. Go to the `list of resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__
2. Change the language, if appropriate
3. Sort by "Untranslated (Descending)"
4. Click on a resource with untranslated strings
5. Click "Untranslated"
6. Read the English text and author the translated text
7. Click "Save Translation" (or press ``TAB``)
8. Repeat from Step 4
9. Notify the Proofreader when strings have been translated

The `Transifex glossary <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/glossary/en/>`__ contains key terms that must be translated consistently. Change the language code at the end of the glossary's URL to view in different languages. It is also available within the translation editor.

It helps to see where the strings appear in context in the `OCDS documentation <https://standard.open-contracting.org/>`__. :doc:`understanding_transifex` describes the link between Markdown files in the `GitHub repository <https://github.com/open-contracting/standard>`__, Transifex resources, and documentation pages. With the exception of the ``schema`` and ``codelists`` resources, you can:

1. Take the name of a resource, e.g. ``schema--changelog``
2. Remove ``--index`` if present
3. Replace ``--`` with ``/``
4. Put it in the pattern ``https://standard.open-contracting.org/{version}/en/{name}/``, like https://standard.open-contracting.org/latest/en/schema/changelog/

.. note::
   Some titles and descriptions of codes are copied from external sources and should not be translated by OCDS. These are tagged as ``should_be_translated_upstream`` and indicated by a small tag icon.

See :ref:`standard/translation/using_transifex:Translation tasks` below for Transifex tips.

Proofreader
~~~~~~~~~~~

1. Go to the `list of resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__
2. Change the language, if appropriate
3. Click "All resources"
4. Click "Unreviewed"
5. Look at the translated text to check its quality (e.g. spelling, grammar, punctuation)
6. If there's a quality issue, update the translated text
7. Notify the Reviewer when strings have been proofread

Reviewer
~~~~~~~~

1.  Go to the `list of resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__
2.  Change the language, if appropriate
3.  Sort by "Unreviewed (Descending)"
4.  Click on a resource with unreviewed strings
5.  Click "Unreviewed"
6.  Read the English text and the translated text and confirm the translation is correct
7.  If there's a translation issue, update the translated text
8.  If there is a Transifex warning (e.g. "Glossary translation for term 'release' missing from translation"), update the translated text
9.  Click "Review"
10. Repeat from Step 4
11. Notify the Coordinator when strings have been reviewed

Translation tasks
-----------------

Translating can be tedious. In general, having more people translating and fewer people reviewing is an efficient way to translate. Beyond that, using shortcuts will make work faster. To see a list of shortcuts, type ``?`` from the translation interface. We cover a few common shortcuts here.

Save current translation and select next string (``TAB``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You'll use this a lot!

Machine translate (``CTRL + h``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Use this carefully, as the strings to translate are specialized. Machine translation works best for short strings that typically require fewer corrections.

Use the highest voted suggestion (``CTRL + u``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Transifex will try to match new source strings with previously translated strings in order to suggest translations. If there is a high percentage match, you may be able to use the suggestion with minimal or no changes.

Copy the source string (``CTRL + g``)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are some strings, in particular very technical terms and names, that aren't translated and for which you can copy the source string.

Check previous translations
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Click the History tab when viewing a string to see its previous translations, when they were edited and by whom. This may inform your current translation, or indicate whom to ask about previous translations.

.. _view-translations-with-warnings:

View translations with warnings
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the `list of resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, click "All resources"
2. Focus on the search box (``Option + s`` or ``ALT + s``)
3. Select "check" from the list of filters
4. Select "warning" from the list of values

View translations with issues
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. From the `list of resources <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, click "All resources"
2. Focus on the search box (``Option + s`` or ``ALT + s``)
3. Select "issue" from the list of filters
4. Select "open" from the list of values

Non-translation tasks
---------------------

Control access permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~

Read Transifex's documentation on `inviting collaborators <https://docs.transifex.com/teams/inviting-collaborators/>`__ and `understanding user roles <https://docs.transifex.com/teams/understanding-user-roles>`__. For more documentation, see `Getting Started as a Localization Manager <https://docs.transifex.com/getting-started/getting-started-as-a-manager>`__.

Approving a team join request assigns the role of "Translator" to the collaborator. Manually assign the role of "Reviewer" if appropriate.

Count untranslated words
~~~~~~~~~~~~~~~~~~~~~~~~

The dashboard of a translation project reports the number of *strings* to translate, but translators must know the number of *words* to translate in order to estimate the time and cost. To get the number of words:

1. Open the translation project
2. Scroll to the list of languages and click "Translate" for a language
3. Click "All resources" at the bottom of the screen
4. Click "# untranslated" at the top of the screen
5. Check the box at the right of the search bar
6. See the number of words at the right of the screen
