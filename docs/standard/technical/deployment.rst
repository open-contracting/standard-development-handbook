Deploying the documentation
===========================

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch versions, as well as non-normative versions.

For changes to the documentation only (no schema changes), start from :ref:`standard/technical/deployment:Merge and release`.

For changes to the theme only, start from :ref:`standard/technical/deployment:Build and deploy`.

To add a community translation, follow :ref:`standard/translation/technical:Add a community translation`.

Schemas and extensions
----------------------

.. note::
   You can skip this section if you are not releasing a new major, minor or patch version.

1. Review extensions
~~~~~~~~~~~~~~~~~~~~

Tidy extensions
^^^^^^^^^^^^^^^

For each *core* extension, :doc:`spell check<spellcheck>`, :doc:`run Markdownlint<lint>`, and ensure it:

-  `Passes its tests <https://github.com/open-contracting/standard-maintenance-scripts/blob/main/badges.md#extensions>`__
-  Matches the description in :ref:`extensions/index:Creating an extension` regarding license, issues and ``README.md``
-  `Has wiki disabled, default branch protected, and topics set <https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration>`__

The following Rake tasks from `standard-maintenance-scripts <https://github.com/open-contracting/standard-maintenance-scripts>`__ will report or correct issues with licenses, issues, ``README.md``, wikis, branches, and topics:

.. code-block:: shell

   bundle exec rake repos:licenses ORG=open-contracting-extensions
   bundle exec rake repos:readmes ORG=open-contracting-extensions
   bundle exec rake fix:lint_repos ORG=open-contracting-extensions
   bundle exec rake fix:protect_branches ORG=open-contracting-extensions
   invoke set-topics

Review pull requests and recent changes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For each *core* extension, review the commits since the last release:

1. Open its homepage on GitHub
2. Open its releases in the sidebar
3. Decide whether to merge pull requests
4. View the commits since the last release (under the release's heading) and consider any substantive changes, i.e. not simple typo or documentation updates

Alternately, run this Rake task to get links to pull requests and comparison URLs:

.. code-block:: shell

   bundle exec rake release:review_extensions ORG=open-contracting-extensions

Create new versions of core extensions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each OCDS version refers to a specific version of each `core extension <https://standard.open-contracting.org/latest/en/extensions/#core-extensions>`__. The `governance process <https://standard.open-contracting.org/latest/en/support/governance/#versions>`__ will establish whether to create a new version of a core extension for this OCDS version.

For each *core* extension for which to create a new version:

1. From the list of releases, click *Draft a new release*
2. In *Tag version*, enter the version number in *vmajor.minor.patch* format, e.g. ``v1.1.1``
3. Enter a summary of changes, e.g. "Typo fixes", and click *Publish release*

Alternately, run this Rake task, which will use the extension's changelog as the release message:

.. code-block:: shell

   bundle exec rake release:release_extensions REF=v1.1.1 REPOS=repo1,repo2

If you make a mistake, you can undo the release with:

.. code-block:: shell

   bundle exec rake release:undo_release_extensions REF=v1.1.1 REPOS=repo1,repo2

Then, add the new releases to the `extension registry <https://github.com/open-contracting/extension_registry>`__. Change to the local directory of the ``extension_registry`` repository, and run:

.. code-block:: shell

   ./manage.py refresh

2. Perform periodic updates, if appropriate
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Update currency codelist
^^^^^^^^^^^^^^^^^^^^^^^^

Before each release, and at least once a year (because ISO4217 is updated `at least once a year <https://github.com/open-contracting/standard/pull/607#issuecomment-339093306>`__), run:

.. code-block:: shell

   python util/fetch_currency_codelist.py

3. Update version numbers, versioned release schema and changelog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In ``docs/conf.py``, update ``release`` to e.g. ``1.1.1`` and update ``version`` if appropriate.

Update the *major__minor__patch* version number:

.. code-block:: shell

   find . \( -name '*.json' -or -name '*.md' -or -name '*.po' \) -exec sed -i "" 's/1__1__3/1__1__4/g' \{\} \;

Update ``versioned-release-validation-schema.json`` and ``dereferenced-release-schema.json`` to match ``release-schema.json``:

.. code-block:: shell

   python util/make_versioned_release_schema.py
   python util/make_dereferenced_release_schema.py

Update ``meta-schema.json`` to match ``meta-schema-patch.json``:

.. code-block:: shell

   python util/make_metaschema.py

4. Set up a development instance of CoVE (OCDS Data Review Tool)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Set up a development instance of CoVE using the new schema, and run tests against it.

Merge and release
-----------------

1. Push and pull updated translations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. :ref:`standard/translation/technical:Push strings to translate to Transifex`.
2. Check all strings are :ref:`translated<standard/translation/using_transifex:Translator>` and :ref:`reviewed<standard/translation/using_transifex:Reviewer>` in supported translations.
3. For any resources with untranslated or unreviewed strings, follow the :doc:`../translation/workflow`.
4. :ref:`standard/translation/using_transifex:View translations with warnings` on Transifex, and correct translated text if necessary.
5. :ref:`Pull supported translations from Transifex<standard/translation/technical:Pull translations from Transifex>`.
6. :ref:`standard/translation/using_transifex:View translations with issues` on Transifex, and correct source and ``.po`` files if necessary.
7. If ``.po`` files were corrected, you may need to :ref:`standard/translation/technical:Push translations to Transifex`.
8. Create a pull request for the updated translation files.
9. :ref:`Test the translations on the build of the pull request<standard/translation/technical:Test translations>`.

.. _merge:

2. Merge the development branch onto the live branch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Create a pull request to merge the development branch into its corresponding live branch, e.g. ``1.1-dev`` into ``1.1``. This might happen by first merging a patch dev branch (``1.1.1-dev``) into the minor dev branch (``1.1-dev``), and then merging into the live branch (``1.1``).
1. Create a pull request to merge the development branch into the ``latest`` branch, if appropriate.

These pull requests can be created throught GitHub's web interface.

3. Create a tagged release
~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.

Create a tagged release named e.g. ``git tag -a 1__1__0 -m '1.1.0 release.'`` and push the tag with ``git push --tags``

.. warning::

   Only tag a commit on a live branch like ``1.1``. Otherwise, the deployment scripts might release older versions of the files.

Build and deploy
----------------

1. Build on continuous integration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`Merging branches<merge>` will trigger a :doc:`build<build>`.

The built documentation is transferred to the staging directory on the server. You can preview the documentation. For example, for OCDS 1.1, https://standard.open-contracting.org/staging/1.1/ is the staging version for https://standard.open-contracting.org/1.1/.

2. Release the documentation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

See the `deploy repository's documentation <https://ocdsdeploy.readthedocs.io/en/latest/deploy/docs.html#publish-released-documentation>`__.

3. Update the Data Review Tool
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

FAQ
---

How can I find out what the standard looked like at 1.0?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

How can I find out what the standard looked like at 1.1.0?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To find a patch release, look at the contents of the tree tagged with that version.
