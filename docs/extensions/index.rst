Extensions
==========

An OCDS release or record package can declare one or more extensions. Extensions extend the standard, by adding new fields, new codelists or new codes to open codelists. Extensions can be brought together as :doc:`profiles<../profiles/index>`.

.. note::

   In principle, the schema are intended to describe correct structure, but are not intended to describe correct data, except in a few cases: for example, in principle, the ``ocid`` field could check for an OCID prefix using a ``pattern`` validation property.

   In practice, a publisher might want to add validation properties to existing fields to describe correct data: for example, constraining addresses, array lengths, etc. Patches that do so are not extensions, but are an acceptable way to do data validation.

Create an extension
-------------------

Follow the instructions in the `extension template <https://github.com/open-contracting/standard_extension_template/blob/master/README.md>`__.

-  Use ``dependencies`` if the extension ``$ref``'erences another extension's definitions.
-  Use ``testDependencies`` if the extension adds fields to another extension's definitions.

If you are creating an extension in an OCP repository:

-  Use the `Apache License 2.0 <https://raw.githubusercontent.com/open-contracting-extensions/ocds_process_title_extension/master/LICENSE>`__
-  Include the following text in its ``README.md`` file:

   .. code-block:: markdown

      ## Issues

      Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.

-  On GitHub:

   -  Protect its default branch
   -  Disable issues (see :ref:`extensions-issues` below)
   -  Disable wiki
   -  Set its topic

The Rake tasks from `standard-maintenance-scripts <https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration>`__ will report or correct issues with the above:

.. code-block:: shell

   bundle exec rake repos:licenses ORG=open-contracting-extensions
   bundle exec rake repos:readmes ORG=open-contracting-extensions
   bundle exec rake fix:protect_branches ORG=open-contracting-extensions
   bundle exec rake fix:lint_repos ORG=open-contracting-extensions
   ./manage.py set-topics

Publish an extension
--------------------

Follow the instructions in the `extension registry <https://github.com/open-contracting/extension_registry>`__.

Change versioned extensions
---------------------------

The versioning of extensions is under discussion in a `pull request <https://github.com/open-contracting/standard/pull/674>`__. For now, see :ref:`standard/technical/deployment:Create new versions of extensions`.

Between OCDS versions, changes can be made to the `'live' version <https://github.com/open-contracting/extension_registry#extension_versionscsv>`__ of a versioned extension; this can be treated as a working draft of a future version.

.. _extensions-issues:

Report issues on extensions
---------------------------

If the issue is with an OCP extension, create an `issue <https://help.github.com/articles/about-issues/>`__ in the `ocds-extensions repository <https://github.com/open-contracting/ocds-extensions>`__. Indicate the extension in the issue's title, e.g. *extension name: issue title*.

.. note::

   Collecting issues in one place gives each more visibility and therefore a higher likelihood of being closed. It also helps to identify related issues across different extensions.

If the issue is with a third-party extension, refer to its documentation.

If the issue is with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), report it on the `standard repository <https://github.com/open-contracting/standard>`__ and add the ``Focus - Extensions`` label.
