Deploying the documentation
===========================

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch versions, as well as non-normative versions.

For changes to the documentation only (no schema changes), start from :ref:`standard/technical/deployment:Merge and release`.

To add a community translation, follow :ref:`standard/translation/technical:Add a community translation`.

Create new versions of extensions
---------------------------------

.. note::
   You can skip this section if you are not releasing a new major, minor or patch version.

The ``conf.py`` file refers to specific versions of some extensions. The `governance process <https://standard.open-contracting.org/latest/en/support/governance/#versions>`__ will establish whether to create new versions of these extensions.

Check for open pull requests and for missing changelog entries. You can run this Rake task to get links to pull requests and comparison URLs:

.. code-block:: shell

   bundle exec rake release:review_extensions ORG=open-contracting-extensions

For each extension for which to create a new version:

#. From the list of releases, click *Draft a new release*
#. In *Tag version*, enter the version number in *vmajor.minor.patch* format, e.g. ``v1.1.1``
#. Enter a summary of changes as the release message, and click *Publish release*

Alternately, run this Rake task, which will use the extension's changelog as the release message:

.. code-block:: shell

   bundle exec rake release:release_extensions REF=v1.1.1 REPOS=repo1,repo2

If you make a mistake, you can undo the release with:

.. code-block:: shell

   bundle exec rake release:undo_release_extensions REF=v1.1.1 REPOS=repo1,repo2

Then, add the new releases to the `extension registry <https://github.com/open-contracting/extension_registry>`__. Change to the local directory of the ``extension_registry`` repository, and run:

.. code-block:: shell

   ./manage.py refresh

Prepare for release
-------------------

.. note::
   You can skip this section if you are not releasing a new major, minor or patch version.

1. Perform maintenance tasks
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See :doc:`maintain`.

2. Perform periodic updates
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before each release, and at least once a year:

-  update external codelists:

.. code-block:: shell

   python manage.py update
 
-  update the country codelist, following the instructions in the ``--help`` message:

.. code-block:: shell

   python manage.py update-country --help

-  check `ISO6523 <https://www.iso.org/standard/25773.html>`__ for new organization identifier schemes:

.. code-block:: shell

   python manage.py check-iso-6523

   - If there are new codes, add them to the `ISO6523-analysis spreadsheet <https://docs.google.com/spreadsheets/d/1qPPAOx9w4NIfrll66a0Qd2SMizoxGNRUMU6YV2rLuEE/edit#gid=1900375069>`__  and update the `Github issue <https://github.com/open-contracting/standard/issues/987>`__ to note that the new codes need to be assessed for inclusion in org-id.guide.

3. Update version numbers, versioned release schema and changelog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In ``docs/conf.py``, update ``release`` to e.g. ``1.1.1`` and update ``version`` if appropriate.

Update the *major__minor__patch* version number:

.. code-block:: shell

   find . \( -name '*.json' -or -name '*.md' -or -name '*.po' \) -exec sed -i "" 's/1__1__3/1__1__4/g' '{}' \;

4. Set up a development instance of CoVE (OCDS Data Review Tool)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set up a development instance of CoVE using the new schema, and run tests against it.

.. _deployment-merge:

Merge and release
-----------------

1. Push and pull updated translations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

#. :ref:`standard/translation/technical:Push strings to translate to Transifex`.
#. Check all strings are :ref:`translated<standard/translation/using_transifex:Translator>` and :ref:`reviewed<standard/translation/using_transifex:Reviewer>` in supported translations.
#. For any resources with untranslated or unreviewed strings, follow the :doc:`../translation/workflow`.
#. :ref:`standard/translation/using_transifex:View translations with warnings` on Transifex, and correct translated text if necessary.
#. :ref:`Pull supported translations from Transifex<standard/translation/technical:Pull translations from Transifex>`.
#. :ref:`standard/translation/using_transifex:View translations with issues` on Transifex, and correct source and ``.po`` files if necessary.
#. If ``.po`` files were corrected, you may need to :ref:`standard/translation/technical:Push translations to Transifex`.
#. Create a pull request for the updated translation files.
#. :ref:`Test the translations on the build of the pull request<standard/translation/technical:Test translations>`.

.. _merge:

2. Merge the development branch onto the live branch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create a pull request to merge the development branch into its corresponding live branch, e.g. ``1.1-dev`` into ``1.1``. This might happen by first merging a patch dev branch (``1.1.1-dev``) into the minor dev branch (``1.1-dev``), and then merging into the live branch (``1.1``). The pull request can be created throught GitHub's web interface.

3. Create a tagged release
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.

#. Create a tag. For example:

   .. code-block:: shell

      git tag -a 1__1__0 -m '1.1.0 release.'

#. Push the tag:

   .. code-block:: shell

      git push --follow-tags

.. warning::

   Only tag a commit on a live branch like ``1.1``. Otherwise, the deployment scripts might release older versions of the files.

Complete the deployment
-----------------------

After :ref:`merging branches<merge>`, GitHub Actions automatically:

-  Deploys the build of any live branch (e.g. ``1.1``) to the live directory (``/home/ocds-docs/web``), as a build directory named ``{branch}-{timestamp}`` (e.g. ``1.1-1577836800``)
-  Creates a symlink named after the live branch (e.g. ``1.1``) that points to the build directory. As such, you can rollback changes by linking to another build directory.
-  Deploys the schema files, codelist files and metadata file (if any), if a tag is pushed: for example, under https://standard.open-contracting.org/schema/, https://standard.open-contracting.org/profiles/ppp/schema/ and https://standard.open-contracting.org/profiles/ppp/extension/.

The live branches are configured in the last step of the repository's ``ci.yml`` workflow.

1. Update the deploy repository
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.

See the `deploy repository's documentation <https://ocdsdeploy.readthedocs.io/en/latest/deploy/docs.html#publish-released-documentation>`__.

2. Update the Data Review Tool
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.

Update the CoVE library
^^^^^^^^^^^^^^^^^^^^^^^

This is the lib-cove-ocds repository for OCDS, and lib-cove-oc4ids for OC4IDS.

-  Update the URL paths in `config.py <https://github.com/open-contracting/lib-cove-ocds/blob/main/libcoveocds/config.py>`__
-  Make sure all tests pass
-  `Release a new version <https://ocp-software-handbook.readthedocs.io/en/latest/python/packages.html#release-process>`__

Update and deploy the Data Review Tool
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This is the cove-ocds repository for OCDS, and cove-oc4ids for OC4IDS.

-  Upgrade the requirements to use the new version of the CoVE library

   .. code-block:: shell

      pip-compile -P libcoveocds; pip-compile requirements_dev.in

-  Update the URL paths in `settings.py <https://github.com/open-contracting/cove-ocds/blob/main/cove_project/settings.py>`__ (*only in cove-ocds*)
-  Make sure all tests pass
-  `Deploy the app <https://ocdsdeploy.readthedocs.io/en/latest/deploy/deploy.html>`__

Update any other tools that use the CoVE library
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Make sure other tools that use ``libcoveocds`` (like Kingfisher Process) are updated to use the new version.

Many tools will use the default options from the library, and these tools will start using the new version of the schema straight away. But if the tool overrides those options with its own options, the tool's own options may need changing.
