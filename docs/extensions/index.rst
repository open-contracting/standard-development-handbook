Extensions
==========

An OCDS release or record package can declare one or more extensions. Extensions extend the standard, by adding new fields, new codelists or new codes to open codelists. Extensions can be brought together as :doc:`profiles<../profiles/index>`.

Creating an extension
---------------------

`Read this draft policy <https://docs.google.com/document/d/1zvR1PDefO6yTK28uKA6XCnxMLiC9oiEeb3uFjHuRyqI/edit>`__ to decide whether to create a `core, community or local extension <https://standard.open-contracting.org/latest/en/extensions/>`__.

To create the extension, `use the extension template <https://github.com/open-contracting/standard_extension_template/blob/main/README.md>`__, which also documents the structure of extensions.

If you're creating an extension in an OCP repository, use the `Apache License 2.0 <https://raw.githubusercontent.com/open-contracting-extensions/ocds_process_title_extension/master/LICENSE>`__, disable issues on the GitHub repository (see :ref:`extensions/index:Reporting issues on extensions` below) and include the following text in its ``README.md`` file:

.. code-block:: markdown

   ## Issues

   Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.

To publish the extension, `add it the extension registry <https://github.com/open-contracting/extension_registry>`__.

Changing *core* extensions
--------------------------

The versioning of core extensions is under discussion in a `pull request <https://github.com/open-contracting/standard/pull/674>`__. For now, see :ref:`standard/technical/deployment:Create new versions of core extensions`.

Between OCDS versions, changes can be made to the `'live' version <https://github.com/open-contracting/extension_registry#extension_versionscsv>`__ of a core extension; this can be treated as a working draft of a future version.

Reporting issues on extensions
------------------------------

`Issues <https://help.github.com/articles/about-issues/>`__ on extensions in OCP repositories should be reported to the `ocds-extensions repository <https://github.com/open-contracting/ocds-extensions>`__. Collecting issues in one place gives each more visibility and therefore a higher likelihood of being closed. It also helps to identify related issues across different extensions. When creating an issue, indicate the extension in the issue's title, e.g. *extension name: issue title*.

To report issues on community extensions, refer to each extension's documentation.

If the issue is with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), report it on the `standard repository <https://github.com/open-contracting/standard>`__ and add the ``Focus - Extensions`` label.
