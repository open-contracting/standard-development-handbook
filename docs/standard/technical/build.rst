Building the documentation
==========================

Get started
-----------

.. code:: eval_rst

   .. note::
      Building the documentation requires Python 3.6.

Create a virtual environment using Python 3.6 with ``pyenv virtualenv docs`` or:

.. code:: shell

   sudo apt-get install python3-venv
   python3 -m venv .ve
   source .ve/bin/activate

Initialize and update submodules:

.. code:: shell

   git submodule init
   git submodule update

Run all commands on this page within this virtual environment.

Install the requirements:

.. code:: shell

   pip install -r requirements.txt

Run tests
---------

The standard repository has tests. Profiles may not.

The standard’s tests must be run after building the documentation:

.. code:: shell

   make
   py.test

Build the documentation
-----------------------

Build the documentation in all languages into ``build/``:

.. code:: shell

   make

Build the source language only:

.. code:: shell

   make source

Build a translation only:

.. code:: shell

   make es

Remove all built files:

::

   make clean

If you changed ``release-schema.json``, update ``versioned-release-validation-schema.json`` (the tests check that this is done):

.. code:: shell

   python util/make_versioned_release_schema.py

Sphinx, which builds the documentation, doesn’t watch directories for changes. To regenerate the documentation whenever changes are made:

-  If you are running macOS and have ``fswatch`` from Homebrew:

   .. code:: shell

      fswatch -0 docs | xargs -0 -n 1 -I {} make

-  If you are running Linux, you can ``pip install watchdog[watchmedo]`` and run:

   .. code:: shell

      watchmedo shell-command --patterns="*.md" --ignore-pattern="build/*" --recursive --command="make"

View the documentation, by running a local web server:

.. code:: shell

   cd build
   python -m http.server

If you are using Firefox you can use the `Live Reload <https://addons.mozilla.org/en-US/firefox/addon/live-reload/>`__ addon to automatically reload the documentation when it changes.

Change the theme
----------------

The theme files are in the `standard_theme <https://github.com/open-contracting/standard_theme>`__ repository, and are part of the virtual environment. Find them in the virtual environment’s directory (e.g. ``.ve/src/standard-theme``).
