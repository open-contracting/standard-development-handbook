Open Contracting for Infrastructure Data Standards
==================================================

`This profile <https://standard.open-contracting.org/infrastructure/latest/en/>`__ is developed and maintained by the Open Contracting Partnership on `GitHub <https://github.com/open-contracting/infrastructure>`__. It is `deployed <https://standard.open-contracting.org/infrastructure/>`__ with the standard documentation. It was previously deployed to https://open-contracting.github.io/infrastructure/, which uses meta refresh to redirect to the current deployment.

Development tasks
-----------------

Copy schema and codelists from OCDS for PPPs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For each new release of OCDS for PPPs, run:

.. code-block:: shell

   make clean_dist
   python schema/borrow-schema.py

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

Install gnumeric:

.. code-block:: shell

   sudo apt install gnumeric
   
On macOS:

.. code-block:: shell

  brew install gnumeric

Create a workbook with a sheet for each mapping CSV file:

.. code-block:: shell

   ssconvert --merge-to=output.xlsx mapping/*.csv

You can then:

* Edit the workbook in your preferred spreadsheet software
* Export each sheet as a CSV file to the `mapping` folder
