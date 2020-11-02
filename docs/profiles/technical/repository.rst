Profile repository
==================

Branches and tags
-----------------

If a profile has adopted a versioning scheme, see the standard’s page for `branches and tags <../../standard/technical/repository.html#branches-and-tags>`__. The only difference is that a profile’s tag names use dots (``1.0.0``) instead of double underscores (``1__0__0``).

If a profile has `moved from ReadTheDocs <integrations>`__, it will have ``99.99`` and ``readthedocs`` protected branches.

Structure
---------

See the standard’s `structure <../../standard/technical/repository.html#structure>`__.

The ```schema/build-profile.py`` <https://github.com/open-contracting/standard_profile_template/blob/master/schema/build-profile.py>`__ script calls the ```build_profile`` method <https://github.com/open-contracting/extension_registry.py/blob/master/ocdsextensionregistry/api.py>`__ in ``extension_registry.py``, which compiles a profile’s extensions into a consolidated extension, storing the results in ``schema/profile``, and extends OCDS with the consolidated extension, storing the results in ``schema/patched``. It also updates the ``codelists`` field in ``extension.json``. All these built files are version controlled.
