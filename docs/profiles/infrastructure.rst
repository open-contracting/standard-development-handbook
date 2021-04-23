Open Contracting for Infrastructure Data Standards
==================================================

`This profile <https://standard.open-contracting.org/infrastructure/latest/en/>`__ is developed and maintained by the Open Contracting Partnership on `GitHub <https://github.com/open-contracting/infrastructure>`__. It is `deployed <https://standard.open-contracting.org/infrastructure/>`__ with the standard documentation. It was previously deployed to https://open-contracting.github.io/infrastructure/, which uses meta refresh to redirect to the current deployment.

Development tasks
-----------------

Copy schema and codelists from OCDS for PPPs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For each new release of OCDS for PPPs, run:

.. code-block:: shell

   python schema/borrow-schema.py
   ocdskit schema-strict schema/project-level/project-schema.json

Update blank.json
~~~~~~~~~~~~~~~~~

Install json-schema-random:

.. code-block:: shell

   npm install git+https://github.com/open-contracting/json-schema-random.git#opencontracting

Update blank.json:

.. code-block:: shell

   node_modules/json-schema-random/cli.js --no-random --no-additional schema/project-level/project-schema.json > docs/examples/blank.json
