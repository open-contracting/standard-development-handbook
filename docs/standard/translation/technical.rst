Technical processes for translation
===================================

This page documents the technical steps to push and pull translations from a translation tool and to build translated schema, codelists and documentation.

You should only perform these tasks once the source files are frozen, after having completed the first steps of the :doc:`deployment process<../technical/deployment>`.

Configure the translation tool
------------------------------

For new major and minor versions, create a new project named, for example: ``open-contracting-standard-1-1``

Extract strings to translate into POT files
-------------------------------------------

If you add, remove or rename a CSV column whose values are translated, you must edit the corresponding ``babel_ocds_*.cfg`` file, as documented by `OCDS Babel <https://ocds-babel.readthedocs.io/en/latest/api/extract.html>`__.

Whenever documentation pages, codelist CSV files or JSON Schema files are changed, you must extract strings to translate from these files into POT files:

.. code-block:: shell

   make extract

If only documentation pages are changed, you may run:

.. code-block:: shell

   make extract_markdown

If only codelist files:

.. code-block:: shell

   make extract_codelists

If only schema files:

.. code-block:: shell

   make extract_schema

Map POT files to resources
--------------------------

Whenever documentation pages, codelist CSV files or JSON Schema files are renamed, added or removed, you must create the POT files as above, and update the translation tool's configuration file.

Use the translation tool
------------------------

-  Push strings to translate to the translation tool
-  Update translations in the translation tool
-  Pull translations from the translation tool

Then, build the documentation with the new translations.

Push translations
-----------------

If text is translated locally by editing PO or POT files, the translations can be pushed to the translation tool, after :doc:`../technical/build`. **This will overwrite any new translations made in the translation tool since the last time they were pulled.**

After pushing, check that the translation progress on the translation tool is minimally affected. To avoid losing translations made on the translation tool, pull translations before applying your changes, re-building the documentation and pushing new translations. If you made a mistake, checkout a clean branch of the standard, re-build the documentation and push old translations.

Test translations
-----------------

Pull requests are built and accessible at ``https://standard.open-contracting.org/staging/BRANCH/``. Translations of Markdown pages using Sphinx directives should be checked in particular:

-  ``es/getting_started/`` uses ``jsoninclude``
-  ``es/schema/reference/`` uses ``jsonschema`` and ``extensionlist``
-  ``es/schema/release/`` has a Docson widget
-  ``es/schema/codelists/`` uses ``csv-table-no-translate``

Review translated codelists
---------------------------

Translated codelists are stored in language directories under ``build/codelists`` during the build process. To stack a list of CSV files for review, you can do:

.. code-block:: bash

   for i in *.csv; do printf "\n\n$i,,,\n\n"; cat $i; done > ../all_codelists.csv

Add a community translation
---------------------------

Once all strings are translated and reviewed in the translation tool, and all warnings or issues in the translation tool are resolved:

#. Checkout the live branch, e.g. ``git checkout 1.1``
#. Checkout a new branch, e.g. ``git checkout -b 1.1-italian``
#. Add the locale code to ``TRANSLATIONS`` in ``include/config.mk``
#. Pull the locale's translations, e.g. ``tx pull -f -l it``
#. Update the ``language_options`` block in ``docs/_templates/layout.html``
#. Create a pull request for the community translation
#. :ref:`Test the translations on the build of the pull request<standard/translation/technical:Test translations>`
#. Merge the new branch onto the live branch
#. :ref:`deployment-merge`, remembering to update ``robots.txt``
