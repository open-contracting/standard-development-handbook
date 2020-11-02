Building the documentation
==========================

Get started
-----------

.. note::
   Building the documentation requires Python 3.6.

Create a virtual environment using Python 3.6 with ``pyenv virtualenv docs`` or:

.. code-block:: shell

   sudo apt-get install python3-venv
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

The standard repository has tests. Profiles may not.

The standard's tests must be run after building the documentation:

.. code-block:: shell

   make
   py.test

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

If you changed ``release-schema.json``, update ``versioned-release-validation-schema.json`` (the tests check that this is done):

.. code-block:: shell

   python util/make_versioned_release_schema.py

Sphinx, which builds the documentation, doesn't watch directories for changes. To regenerate the documentation whenever changes are made:

-  If you are running macOS and have ``fswatch`` from Homebrew:

   .. code-block:: shell

      fswatch -0 docs | xargs -0 -n 1 -I {} make

-  If you are running Linux, you can ``pip install watchdog[watchmedo]`` and run:

   .. code-block:: shell

      watchmedo shell-command --patterns="*.md" --ignore-pattern="build/*" --recursive --command="make"

View the documentation, by running a local web server:

.. code-block:: shell

   cd build
   python -m http.server

If you are using Firefox you can use the `Live Reload <https://addons.mozilla.org/en-US/firefox/addon/live-reload/>`__ addon to automatically reload the documentation when it changes.

Change the theme
----------------

The theme files are in the `standard_theme <https://github.com/open-contracting/standard_theme>`__ repository, and are part of the virtual environment. Find them in the virtual environment's directory (e.g. ``.ve/src/standard-theme``).
