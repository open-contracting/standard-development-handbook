Building the documentation
==========================

Get started
-----------

.. note::

   Building the documentation requires Python 3.8 or greater.

Create a virtual environment using Python 3 with ``pyenv virtualenv docs`` or:

.. code-block:: shell

   sudo apt install python3-venv
   python3 -m venv .ve
   source .ve/bin/activate

Initialize and update submodules:

.. code-block:: shell

   git submodule init
   git submodule update

.. note::

   If you need to change a submodule, it's simplest to edit ``.gitmodules``, remove the submodule, then run the above. For example:

   .. code-block:: shell

      rm -rf .git/modules
      rm -rf path/to/submodule
      git submodule init
      git submodule update
      cd path/to/submodule
      git checkout desired-branch

Run all commands on this page within this virtual environment.

Install the requirements:

.. code-block:: shell

   pip install -r requirements.txt

Run tests
---------

Build the documentation:

.. code-block:: shell

   make

Run the tests:

.. code-block:: shell

   pytest

To replicate the GitHub Actions workflow, you also need to `run the tests from the standard maintenance scripts <https://github.com/open-contracting/standard-maintenance-scripts#tests>`__.

``test_search`` will report failures if you have not yet pushed your branch to GitHub because the search index is only built for a branch once you push it. Once your PR passes, the local tests are expected to pass.

Troubleshoot
~~~~~~~~~~~~

If the tests are failing:

-  Ensure your dependencies are up-to-date:

   .. code-block:: shell

      pip install -r requirements_dev.txt

-  Clean and re-build the documentation:

   .. code-block:: shell

      make clean
      make

Build the documentation
-----------------------

Build the documentation in all languages into ``build/``:

.. code-block:: shell

   make

Build the source language only:

.. code-block:: shell

   make source

Build a translation only:

.. code-block:: shell

   make es

Remove all built files:

.. code-block:: shell

   make clean

If you edited ``release-schema.json`` or ``meta-schema-patch.json``, update files with:

.. code-block:: shell

   python manage.py pre-commit

Sphinx, which builds the documentation, doesn't watch directories for changes. To regenerate the documentation and refresh the browser whenever changes are made, run:

.. code-block:: shell

   make autobuild

Otherwise, view the documentation by running a local web server:

.. code-block:: shell

   python -m http.server --directory build
