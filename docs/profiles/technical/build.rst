Building the documentation
==========================

See the standard's page for :doc:`../../../standard/technical/build`.

Change version of OCDS
----------------------

1. Change ``standard_tag`` and ``standard_version`` in ``conf.py`` to the desired version of OCDS
2. Update the versions of extensions in ``extension_versions.json``, if appropriate
3. :ref:`profiles/technical/build:Build the profile`

Change extensions
-----------------

To change the extensions in a profile, change ``extension_versions.json``, then :ref:`profiles/technical/build:Build the profile`.

Extensions must be in the `extension registry <https://github.com/open-contracting/extension_registry>`__ and should be tagged and released. See :ref:`standard/technical/deployment:Create new versions of extensions`.

Build the profile
-----------------

.. code-block:: shell

   make update

See :doc:`repository` for information on what files are built by this command.
