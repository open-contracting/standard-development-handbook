Translation
===========

.. seealso::

   The standard's page for :doc:`../../../standard/translation/index`

The instructions below are similar to others in `ocds-extensions-translations <https://github.com/open-contracting/ocds-extensions-translations#populate-initial-translations>`__. They will, at minimum, pre-translate the text from the unextended schema and codelists.

Pre-translate a profile
-----------------------

One-time setup
~~~~~~~~~~~~~~

#. Install ``translate-toolkit``:

   .. code-block:: bash

      brew install translate-toolkit

#. Install ``python-Levenshtein``:

   .. code-block:: bash

      eval $(brew --prefix translate-toolkit)/libexec/bin/python -m pip install python-Levenshtein

#. Clone the `standard <https://github.com/open-contracting/standard>`__ and `ocds-extensions-translations <https://github.com/open-contracting/ocds-extensions-translations>`__ repositories into the same parent directory:

   .. code-block:: bash

      git clone git@github.com:open-contracting/standard.git
      git clone git@github.com:open-contracting/ocds-extensions-translations.git

Each-time setup
~~~~~~~~~~~~~~~

#. Set the ``lang`` environment variable, for example:

   .. code-block:: bash

      lang=es
      wip=path/to/profile/from/standard

Prepare the compendia
~~~~~~~~~~~~~~~~~~~~~

#. Change to the ``standard`` directory, then prepare a compendium:

   .. code-block:: bash

      git checkout 1.1
      git pull --rebase
      msgcat --use-first docs/locale/$lang/**.po > $wip/$lang-standard.po
      git checkout 1.1-dev

#. Change to the ``ocds-extensions-translations`` directory, then prepare a compendium. For example, for OCDS for PPPs 1.0.0-beta3:

   .. code-block:: bash

      git checkout main
      git pull --rebase
      for extension_version in bids/v1.1.5 charges/master documentation_details/master finance/master location/v1.1.5 metrics/1.1 milestone_documents/v1.1.5 performance_failures/master project/master risk_allocation/master shareholders/master signatories/master tariffs/1.1 ppp/master; do
        msgcat --use-first locale/$lang/LC_MESSAGES/$extension_version/**.po > $lang-$(echo $extension_version | tr '/' '-').po
      done
      msgcat --use-first $(ls $lang-*.po) > $wip/$lang-extensions.po
      rm -f $lang-*.po

#. Change to the profile's directory, then prepare a compendium:

   .. code-block:: bash

      if [ -d docs/locale/$lang/LC_MESSAGES ]; then
        msgcat --use-first $lang-standard.po $lang-extensions.po docs/locale/$lang/**.po > $lang.po
      else
        msgcat --use-first $lang-standard.po $lang-extensions.po > $lang.po
      fi

Pre-translate the profile
~~~~~~~~~~~~~~~~~~~~~~~~~

#. Count untranslated messages:

   .. code-block:: bash

      pocount --incomplete docs/locale/$lang/LC_MESSAGES | tail -n 10

#. Create the POT files:

   .. code-block:: bash

      make extract

#. Re-create the PO files:

   .. code-block:: bash

      rm -rf docs/locale/$lang/LC_MESSAGES
      sphinx-intl update -p build/locale -d docs/locale -l $lang

#. Pre-populate the PO files:

   .. code-block:: bash

      cd docs/locale/$lang/LC_MESSAGES
      for f in **.po; do
        pretranslate --nofuzzymatching -t ../../../../$lang.po ../../../../build/locale/{$f}t $f
      done
      cd ../../../..

#. Count untranslated messages:

   .. code-block:: bash

      pocount --incomplete docs/locale/$lang/LC_MESSAGES | tail -n 10

#. Clean up:

   .. code-block:: bash

      rm -f $lang-standard.po $lang-extensions.po $lang.po

Technical implementation of translation
---------------------------------------

.. seealso::

   The standard's page for :doc:`../../../standard/translation/implementation`

-  ``babel_ocds_codelist.cfg`` indicates the codelist CSV files in the consolidated extension and the patched OCDS (``schema/*/codelists/*.csv``) from which to extract strings to translate.
-  ``babel_ocds_schema.cfg`` indicates the JSON Schema files in the consolidated extension and the patched OCDS (``schema/*/*-schema.json``) from which to extract strings to translate.
-  ``conf.py`` calls ``translate`` to translate the JSON Schema files and codelist CSV files from ``schema/profile`` to ``build/<lang>``, and from ``schema/patched`` to ``docs/_static/patched``.
