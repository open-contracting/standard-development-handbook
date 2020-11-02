Deployment
==========

A profile’s deployment is the same as the standard’s `deployment <../../standard/technical/deployment>`__, except where noted below. If a profile is unversioned, some of the below may be irrelevant.

Schemas and extensions
----------------------

1. Review extensions
~~~~~~~~~~~~~~~~~~~~

Review pull requests and recent changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Follow the `standard’s instructions <../../standard/technical/deployment.html#review-pull-requests-and-recent-changes>`__, substituting the profile’s extensions for core extensions.

Create new releases of core extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The governance process will establish whether to create a new release of any core extensions within the profile. If appropriate, follow the `standard’s instructions <../../standard/technical/deployment.html#create-new-versions-of-core-extensions>`__.

2. Perform periodic updates, if appropriate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Check the profile’s individual handbook page for any regular maintenance.

3. Update version numbers, versioned release schema and changelog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In ``docs/conf.py``, update ``release`` to e.g. ``1.0.0`` and update ``version`` if appropriate.

Update the \*major__minor__patch\* version number:

.. code:: shell

   find . \( -name '*.json' -or -name '*.md' -or -name '*.po' \) -exec sed -i "" 's/1__0__0__beta/1__0__0/g' \{\} \;

Update the profile’s changelog (if any) with a summary of the changes to the profile’s extensions.

4. Integrate extensions
~~~~~~~~~~~~~~~~~~~~~~~

`Build the profile <build.html#build-the-profile>`__.
