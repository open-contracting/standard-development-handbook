Open Contracting for Infrastructure Data Standards
==================================================

`This profile <https://standard.open-contracting.org/infrastructure/latest/en/>`__ is developed and maintained by the Open Contracting Partnership on `GitHub <https://github.com/open-contracting/infrastructure>`__. It is `deployed <https://standard.open-contracting.org/infrastructure/>`__ with the standard documentation. It was previously deployed to https://open-contracting.github.io/infrastructure/, which uses meta refresh to redirect to the current deployment.

Maintenance
-----------

Copy schema and codelists from OCDS for PPPs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For each new release of OCDS for PPPs, run:

.. code-block:: shell

   make update

Review the changes. If there were updates to the OC4IDS copy of shared fields and codelists since the last release of OCDS for PPPs, you may need to update the `update` function in `manage.py` accordingly.

To use a pre-release of OCDS for PPPs, run:

.. code-block:: shell

   ./manage.py update --ppp-base-url https://standard.open-contracting.org/staging/profiles/ppp/1.0-dev/en/_static/patched/

Update blank.json
~~~~~~~~~~~~~~~~~

Install json-schema-random:

.. code-block:: shell

   npm install git+https://github.com/open-contracting/json-schema-random.git#opencontracting

Update blank.json:

.. code-block:: shell

   node_modules/json-schema-random/cli.js --no-random --no-additional schema/project-level/project-schema.json > docs/examples/blank.json

Create a workbook with a sheet for each mapping CSV file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are making many changes to the mapping CSV files, you might want to create a workbook containing a sheet for each CSV file.

Install gnumeric on Ubuntu:

.. code-block:: shell

   sudo apt install gnumeric
   
Or, on macOS:

.. code-block:: shell

   brew install gnumeric

Create a workbook with one sheet per mapping CSV file:

.. code-block:: shell

   ssconvert --merge-to=output.xlsx mapping/*.csv

You can then:

-  Edit the workbook in your preferred spreadsheet software
-  Export each sheet as a CSV file to the ``mapping`` directory

Update sustainability.yaml
~~~~~~~~~~~~~~~~~~~~~~~~~~

For each change to the `CoST IDS sustainability elements <https://docs.google.com/spreadsheets/d/165epI69oQ5YyL4-2q8VubFn9VuNham2Pi1u0P49id9o/>`__, run:

.. code-block:: shell

  ./manage.py update-sustainability-elements

Update sustainability.md
~~~~~~~~~~~~~~~~~~~~~~~~

For each change to ``mapping/sustainability.yaml``:

1. Lint it, and link any field names to the schema reference documentation:

.. code-block:: shell

  ./manage.py lint -l mapping/sustainability.yaml

2. Update ``docs/cost/ids/sustainability.md``:

.. code-block:: shell

  ./manage.py update-sustainability-docs
