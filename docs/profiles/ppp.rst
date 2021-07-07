Public Private Partnerships
===========================

`This profile <https://standard.open-contracting.org/profiles/ppp/latest/en/>`__ is developed and maintained by the Open Contracting Partnership on `GitHub <https://github.com/open-contracting-extensions/public-private-partnerships>`__. It is `deployed <https://standard.open-contracting.org/profiles/ppp/>`__ with the standard documentation. It was previously deployed to https://ocds-for-ppps.readthedocs.io/, which uses meta refresh to redirect to the current deployment.

Maintenance
-----------

Change extensions or version of OCDS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See :doc:`technical/build` to:

-  Change version of OCDS
-  Change extensions
-  Build the profile

In ``codelists.md``:

-  Update the version numbers in the links to extensions' documentation, if appropriate.
-  If extensions or OCDS add or remove codelists, add or remove sections as appropriate.

To find codelists to add or remove, run (in Bash):

.. code-block:: shell

   diff -u <(ls -1 schema/profile/codelists | sed 's/^[+-]//' | sort | uniq) <(grep :file: docs/reference/codelists.md | cut -d'/' -f 5 | sort)

Translation
-----------

See the generic profile documentation for :doc:`translation`.

For reference:

-  The translations of the patched OCDS's codelists are used by ``codelists.md`` and ``documents.md``.
-  The translation of the patched OCDS's release schema is used by ``framework.md``, ``documents.md`` and ``schema.md``
