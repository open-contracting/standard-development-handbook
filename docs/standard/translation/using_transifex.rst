Using Transifex
===============

Steps for translators, proofreaders and reviewers
-------------------------------------------------

Translator
~~~~~~~~~~

.. admonition:: OCDS only

   Before beginning, ask the :ref:`Coordinator<roles>` to ensure that the :ref:`Transifex glossary<glossary>` is up-to-date. If the glossary is not yet available in your language, ask the Coordinator to arrange it.

#. Go to the list of resources (`OCDS <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, `OC4IDS <https://www.transifex.com/open-contracting-partnership-1/oc4ids-09/translate/#es>`__)
#. Change the language, if appropriate
#. Sort by "Untranslated (Descending)"
#. For all resources with untranslated strings:

   #. Click on the resource
   #. Click "Untranslated"
   #. Read the English text and author the translated text

      .. warning::

         Follow the :ref:`translation-style-guide`. In particular, do not translate:

         -  words in backticks, like \`title\` (often used for schema fields)
         -  words in single quotes, like 'open' (often used for codelist codes)
         -  relative URLs, like ``[translate this](#but-not-this)``

         And do not change:

         -  Markdown formatting
         -  Punctuation
         -  Whitespace

         Absolute URLs (that is, starting with ``https://``) can be translated: for example, if the website offers content in multiple languages.

   #. Click "Save Translation" (or press ``TAB``)

#. Repeat from Step 4
#. Notify the Proofreader when strings have been translated

It helps to see where the strings appear in context in the documentation (`OCDS <https://standard.open-contracting.org/>`__, `OC4IDS <https://standard.open-contracting.org/infrastructure/>`__). :doc:`understanding_transifex` describes the link between GitHub files (`OCDS <https://github.com/open-contracting/standard>`__, `OC4IDS <https://github.com/open-contracting/infrastructure>`__), Transifex resources, and documentation pages. For Transifex resources related to :ref:`Markdown files<markdown-resources>`, you can:

#. Take the name of a resource, like ``history--changelog`` or ``reference--changelog``
#. Remove ``--index`` if present
#. Replace ``--`` with ``/``
#. Put it in a pattern below, substituting ``{version}`` for the version of the standard you are translating:

   OCDS
     ``https://standard.open-contracting.org/staging/{version}/en/{name}/``, like https://standard.open-contracting.org/staging/1.2-dev/en/history/changelog/
   OC4IDS
     ``https://standard.open-contracting.org/staging/infrastructure/{version}/en/{name}/``, like https://standard.open-contracting.org/staging/infrastructure/0.9-dev/en/reference/changelog/

See :ref:`standard/translation/using_transifex:Translation tasks` below for Transifex tips.

Proofreader
~~~~~~~~~~~

#. Go to the list of resources (`OCDS <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, `OC4IDS <https://www.transifex.com/open-contracting-partnership-1/oc4ids-09/translate/#es>`__)
#. Change the language, if appropriate
#. Click "All resources"
#. Click "Unreviewed"
#. Look at the translated text to check its quality (e.g. spelling, grammar, punctuation)
#. If there's a quality issue, update the translated text
#. Notify the Reviewer when strings have been proofread

Reviewer
~~~~~~~~

#. Go to the list of resources (`OCDS <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, `OC4IDS <https://www.transifex.com/open-contracting-partnership-1/oc4ids-09/translate/#es>`__)
#. Change the language, if appropriate
#. Sort by "Unreviewed (Descending)"
#. For all resources with unreviewed strings:

   #. Click on the resource
   #. Click "Unreviewed"
   #. Read the English and translated texts, and confirm the translation is correct
   #. If there's a translation issue, update the translated text
   #. If there is a Transifex warning (like "Glossary translation for term 'release' missing from translation"), update the translated text
   #. Click "Review"

#. Notify the Coordinator when strings have been reviewed

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

#. From the list of resources (`OCDS <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, `OC4IDS <https://www.transifex.com/open-contracting-partnership-1/oc4ids-09/translate/#es>`__), click "All resources"
#. Focus on the search box (``Option + s`` or ``ALT + s``)
#. Select "check" from the list of filters
#. Select "warning" from the list of values

View translations with issues
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. From the list of resources (`OCDS <https://www.transifex.com/open-contracting-partnership-1/open-contracting-standard-1-1/translate/#es>`__, `OC4IDS <https://www.transifex.com/open-contracting-partnership-1/oc4ids-09/translate/#es>`__), click "All resources"
#. Focus on the search box (``Option + s`` or ``ALT + s``)
#. Select "issue" from the list of filters
#. Select "open" from the list of values

Non-translation tasks
---------------------

Control access permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~

Read Transifex's documentation on `inviting collaborators <https://help.transifex.com/en/articles/6223451-inviting-collaborators>`__ and `understanding user roles <https://help.transifex.com/en/articles/6223416-understanding-user-roles>`__. For more documentation, see `Getting Started as a Localization Manager <https://help.transifex.com/en/collections/3519161-localization-guides-tips#getting-started-as-a-localization-manager>`__.

Approving a team join request assigns the role of "Translator" to the collaborator. Manually assign the role of "Reviewer" if appropriate.

Count untranslated words
~~~~~~~~~~~~~~~~~~~~~~~~

The dashboard of a translation project reports the number of *strings* to translate, but translators must know the number of *words* to translate in order to estimate the time and cost. To get the number of words:

#. Open the translation project
#. Scroll to the list of languages and click "Translate" for a language
#. Click "All resources" at the bottom of the screen
#. Click "# untranslated" at the top of the screen
#. Check the box at the right of the search bar
#. See the number of words at the right of the screen
