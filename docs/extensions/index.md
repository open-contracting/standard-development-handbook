# Extensions

An OCDS release or record package can declare one or more extensions. Extensions extend the standard, by adding new fields, new codelists or new codes to open codelists. Extensions can be brought together as [profiles](../profiles).

## Creating an extension

[Read this draft policy](https://docs.google.com/document/d/1zvR1PDefO6yTK28uKA6XCnxMLiC9oiEeb3uFjHuRyqI/edit) to decide whether to create a [core, community or local extension](http://standard.open-contracting.org/latest/en/extensions/).

To create the extension, [use the extension template](https://github.com/open-contracting/standard_extension_template/blob/master/README.md), which also documents the structure of extensions.

If you're creating a *core* extension, use the [Apache License 2.0](https://raw.githubusercontent.com/open-contracting/ocds_process_title_extension/master/LICENSE), disable issues on the GitHub repository (see [reporting issues on extensions](#reporting-issues-on-extensions) below) and include the following text in its `README.md` file:

```markdown
## Issues

Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.
```

To publish the extension, [add it the extension registry](https://github.com/open-contracting/extension_registry).

## Changing *core* extensions

The versioning of core extensions is under discussion in a [pull request](https://github.com/open-contracting/standard/pull/674). For now, see [creating new versions of core extensions](../standard/technical/deployment#create-new-versions-of-core-extensions).

Between OCDS versions, changes can be made to the ['live' version](https://github.com/open-contracting/extension_registry#extension_versionscsv) of a core extension; this can be treated as a working draft of a future version.

## Reporting issues on extensions

[Issues](https://help.github.com/articles/about-issues/) on *core* extensions should be reported to the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions). Collecting issues in one place gives each more visibility and therefore a higher likelihood of being closed. It also helps to identify related issues across different extensions. When creating an issue, indicate the extension in the issue's title, e.g. *extension name: issue title*.

To report issues on community extensions, refer to each extension's documentation.

If the issue is with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), report it on the [`standard` repository](https://github.com/open-contracting/standard) and add the `Focus - Extensions` label.
