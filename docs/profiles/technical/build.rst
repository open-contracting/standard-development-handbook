Building the documentation
==========================

.. seealso::

   The standard's page for :doc:`../../../standard/technical/build`

Change OCDS version
-------------------

#. Change ``standard_tag`` and ``standard_version`` in ``conf.py`` to the desired version of OCDS
#. Update the versions of extensions in ``extension_versions.json``, if appropriate
#. :ref:`profiles/technical/build:Build the profile`

Change extensions
-----------------

#. Edit ``extension_versions.json``
#. :ref:`profiles/technical/build:Build the profile`

.. note::

   Extension versions must be in the `extension registry <https://github.com/open-contracting/extension_registry>`__. See :ref:`standard/technical/deployment:Create new versions of extensions`.

Build the profile
-----------------

.. code-block:: shell

   make update

See :doc:`repository` for information on what files are built by this command.
