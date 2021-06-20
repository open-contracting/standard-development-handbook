Profile repository
==================

Branches and tags
-----------------

If a profile has adopted a versioning scheme, see the standard's page for :ref:`standard/technical/repository:Branches and tags`. The only difference is that a profile's tag names use dots (``1.0.0``) instead of double underscores (``1__0__0``).

If a profile has :doc:`moved from ReadTheDocs<integrations>`, it will have ``99.99`` and ``readthedocs`` protected branches.

Structure
---------

See the standard's :ref:`standard/technical/repository:Structure`.

The `manage.py <https://github.com/open-contracting/standard_profile_template/blob/latest/manage.py>`__ script called by ``make update`` calls the `build_profile method <https://ocdsextensionregistry.readthedocs.io/en/latest/api/api.html>`__ in ``extension_registry.py``, which compiles a profile's extensions into a consolidated extension, storing the results in ``schema/profile``, and extends OCDS with the consolidated extension, storing the results in ``schema/patched``. It also updates the ``codelists`` field in ``extension.json``. All these built files are version controlled.
