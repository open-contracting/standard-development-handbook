Technical implementation of translation
=======================================

This page documents the code involved in translating files. It is only necessary to read this page if you are editing or debugging these technical processes. Otherwise, the steps have been simplified and abstracted into the two commands ``make extract`` and ``make``, covered under :doc:`technical` and :doc:`../technical/build`.

.. note::
   We use the `gettext <https://en.wikipedia.org/wiki/Gettext>`_ system for translation. In gettext, strings to translate are referred to as 'messages', and messages are collected into 'domains', which correspond to POT files.

Extract messages
----------------

First, strings to translate are extracted from files with ``make extract``.

Extract from Codelist CSV files and JSON Schema files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. `make extract <https://github.com/open-contracting/standard_profile_template/blob/latest/include/common.mk>`__ builds the ``extract_codelists`` and ``extract_schema`` Make targets, among others. These run:

   .. code-block:: shell

       pybabel extract -F babel_ocds_codelist.cfg . -o $(POT_DIR)/$(DOMAIN_PREFIX)codelists.pot
       pybabel extract -F babel_ocds_schema.cfg . -o $(POT_DIR)/$(DOMAIN_PREFIX)schema.pot

#. `pybabel extract <https://babel.pocoo.org/en/latest/cmdline.html#extract>`__ extracts messages from source files and generates a POT file. The ``-F`` (``--mapping-file``) option sets the path to the Babel mapping configuration file, ``babel_ocds_codelist.cfg`` or ``babel_ocds_schema.cfg``.

#. The `Babel mapping configuration files <https://babel.pocoo.org/en/latest/messages.html#extraction-method-mapping-and-configuration>`__, ``babel_ocds_codelist.cfg`` and ``babel_ocds_schema.cfg``, map Babel message extraction method names – ``ocds_codelist`` and ``ocds_schema`` – to the codelist CSV and JSON Schema source files from which to extract strings to translate.

#. `setup.py in ocds-babel <https://github.com/open-contracting/ocds-babel/blob/main/setup.py>`__ maps the `Babel message extraction method names <https://babel.pocoo.org/en/latest/messages.html#writing-extraction-methods>`__ – ``ocds_codelist`` and ``ocds_schema`` – to the module and function implementing the extraction, in the entry point group ``babel.extractors``.

#. The functions `extract_codelist and extract_schema <https://github.com/open-contracting/ocds-babel/blob/main/ocds_babel/extract.py>`__ implement the extraction.

Extract from Markdown files
~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. ``make extract`` builds the ``extract_markdown`` Make target, among others. This runs:

   .. code-block:: shell

       sphinx-build -q -b gettext $(DOCS_DIR) $(POT_DIR)

See the `Sphinx documentation <https://www.sphinx-doc.org/en/master/intl.html#sphinx-internationalization-details>`__.

Translate source files
----------------------

After pushing strings to translate as POT files to Transifex, :doc:`translating the strings<workflow>`, and pulling translations as PO files from Transifex, source files are translated with ``make``.

Translate Codelist CSV files and JSON Schema files
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. `make <https://github.com/open-contracting/standard_profile_template/blob/latest/include/common.mk>`__ builds the ``compile`` Make target. This compiles to MO files the PO files for codelist CSV files and JSON Schema files.

   .. code-block:: shell

       pybabel compile --use-fuzzy -d $(LOCALE_DIR) -D $(DOMAIN_PREFIX)schema
       pybabel compile --use-fuzzy -d $(LOCALE_DIR) -D $(DOMAIN_PREFIX)codelists

#. ``make`` then builds ``build.*`` Make targets, among others. These run, for example:

   .. code-block:: shell

       sphinx-build -q -b dirhtml $(DOCS_DIR) $(BUILD_DIR)/es -D language="es"

#. `sphinx-build <https://www.sphinx-doc.org/en/master/man/sphinx-build.html>`__, when ``language`` is set, compiles to MO files the PO files for Markdown files, which can also be done by running ``sphinx-intl build -d $(LOCALE_DIR)``.

#. `sphinx-build <https://www.sphinx-doc.org/en/master/man/sphinx-build.html>`__ runs ``setup`` in ``conf.py``, which reads the ``language`` override (``-D language="es"``).

#. `setup in conf.py <https://github.com/open-contracting/standard_profile_template/blob/latest/docs/conf.py>`__ calls the `translate method <https://github.com/open-contracting/ocds-babel/blob/main/ocds_babel/translate.py>`__ to translate codelist CSV files and JSON Schema files from one directory into another directory, using MO files.

#. The translated files are used by Sphinx directives like ``csv-table-no-translate`` and ``jsonschema`` in Markdown files.

Translate Markdown files
~~~~~~~~~~~~~~~~~~~~~~~~

#. ``make`` builds the ``build.*`` Make targets, among others. These run, for example:

   .. code-block:: shell

       sphinx-build -q -b dirhtml $(DOCS_DIR) $(BUILD_DIR)/es -D language="es"

See the `Sphinx documentation <https://www.sphinx-doc.org/en/master/intl.html#sphinx-internationalization-details>`__.

Please correct all warnings, ignoring ``WARNING: inconsistent term references in translated message``.
