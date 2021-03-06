Technical processes for translation
===================================

This page documents the technical steps to push and pull translations from Transifex and to build translated schema, codelists and documentation.

You should only perform these tasks once the source files are frozen, after having completed :ref:`standard/technical/deployment:Schemas and extensions` in the deployment process.

Configure Transifex
-------------------

Credentials
~~~~~~~~~~~

The first time you use Transifex, create a `~/.transifexrc file <https://docs.transifex.com/client/client-configuration#~/-transifexrc>`__ (replace ``USERNAME`` and ``PASSWORD``):

.. code-block:: shell

   sphinx-intl create-transifexrc --transifex-username USERNAME --transifex-password PASSWORD

Projects
~~~~~~~~

For new major and minor versions:

-  `Create a Transifex project <https://www.transifex.com/open-contracting-partnership-1/>`__, named e.g. ``open-contracting-standard-1-1``

   -  In the *Add a new project* screen, under *Choose privacy type*, select ``Public project`` and tick the box marked ``My project is a non-commercial Open Source project``.

-  Update ``TRANSIFEX_PROJECT`` in ``include/config.mk`` with the name of the Transifex project

Extract strings to translate into POT files
-------------------------------------------

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

Map POT files to Transifex resources
------------------------------------

Whenever documentation pages, codelist CSV files or JSON Schema files are renamed, added or removed, you must create the POT files as above, empty the `.tx/config file <https://docs.transifex.com/client/client-configuration#-tx/config>`__ (``make clean_txconfig``) and update the ``.tx/config`` file (``make update_txconfig``). In short, run:

.. code-block:: shell

   make extract clean_txconfig update_txconfig

Push strings to translate to Transifex
--------------------------------------

To push POT files, run ``tx push -s``. To both extract strings and push resources, run:

.. code-block:: shell

   make push

To push specific resources (replace the Transifex project name), run e.g.:

.. code-block:: shell

   tx push -s -r open-contracting-standard-1-1.codelists open-contracting-standard-1-1.schema

Pull translations from Transifex
--------------------------------

To forcefully pull *supported* translations, run ``make pull`` or ``tx pull -f -l es``

To forcefully pull *specific* translations, run e.g. ``make pull.es`` or ``tx pull -f -l es``

To forcefully pull *all* translations, run ``tx pull -f -a``

Then, build the documentation with the new translations.

Push translations to Transifex
------------------------------

If text is translated locally by editing PO or POT files, the translations can be pushed to Transifex, after :doc:`../technical/build`. **This will overwrite any new translations made on Transifex since the last time they were pulled.** Run ``make force_push`` or ``tx push -s -t -f -l es --no-interactive``

After pushing, check that the translation progress on Transifex is minimally affected. To avoid losing translations made on Transifex, pull translations before applying your changes, re-building the documentation and pushing new translations. If you made a mistake, checkout a clean branch of the standard, re-build the documentation and push old translations.

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

Once all strings are translated and reviewed in Transifex, and all warnings or issues on Transifex are resolved:

1.  Checkout the live branch, e.g. ``git checkout 1.1``
2.  Checkout a new branch, e.g. ``git checkout -b 1.1-italian``
3.  Add the locale code to ``TRANSLATIONS`` in ``include/config.mk``
4.  Pull the locale's translations, e.g. ``tx pull -f -l it``
5.  Update the ``language_options`` block in ``docs/_templates/layout.html``
6.  Create a pull request for the community translation
7.  :ref:`Test the translations on the build of the pull request<standard/translation/technical:Test translations>`
8.  Check the ``localization-note`` appears on the homepage
9.  Merge the new branch onto the live branch
10. :ref:`standard/technical/deployment:Build and deploy`, remembering to update ``robots.txt``
