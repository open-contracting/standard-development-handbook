# Extensions

An OCDS release or record package may declare one or more extensions. Extensions can add to the schema, add new codelists, or add entries to existing codelists. 

See the [standard documentation](http://standard.open-contracting.org/latest/en/extensions/) for definitions of core, community and local extensions.

In addition, a collection of extensions may be packaged together as an **OCDS profile**. When used as part of a profile, extensions may additionally: remove scheme elements and codelist entries. 

The structure of an extension is documented via the [standard extension template](https://github.com/open-contracting/standard_extension_template/blob/master/README.md).

## When to create a *core* extension

* An extension can be authored to limit 'scope creep' of the core standard, especially in cases where we lack implementation experience with the proposed changes. The extension may serve as a way to externalize the risk of permanent changes to the core standard.
* An extension may lower risks associated to the 'compliance mindset' (e.g. if a publisher sees bids in the standard but is prevented by law from publishing bids, they may object to adopting the standard entirely).
* An extension externalizes confusing, complex, or non-universal concepts. For example, lots are not universal and may be complex. Gazetteers (as in the location extension) are not universal.
* An extension can be a means of breaking backwards compatibility (for example, removing codes from codelists), which would otherwise require a 2.0 version of OCDS.

## Creating extensions

It is recommended to use the [standard extension template](https://github.com/open-contracting/standard_extension_template). All *core* extensions are released under the [Apache License 2.0](https://raw.githubusercontent.com/open-contracting/ocds_process_title_extension/master/LICENSE).

The mechanism for extending a core JSON Schema file, like `release-schema.json`, is to author a small, similar-looking JSON Schema file, that is applied to the core file using [JSON Merge Patch](https://tools.ietf.org/html/rfc7396).

When creating a [*core* extension](http://standard.open-contracting.org/latest/en/extensions/#core-extensions), the GitHub repository should have issues disabled (see [reporting issues on extensions](#reporting-issues-on-extensions) below). Its `README.md` file should include the following text:

```markdown
## Issues

Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.
```

When creating a [community extension](http://standard.open-contracting.org/latest/en/extensions/#community-extensions), there are no requirements regarding issues.

## Publishing extensions

Once an extension is created, it should be added to the extension registry - an inventory of extensions that is included in the [standard's documentation](http://standard.open-contracting.org/latest/en/extensions/) - [as described in its readme](https://github.com/open-contracting/extension_registry).

### Publishing new versions of extensions

The [*core* extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) are versioned using [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) and made available as [releases on GitHub](https://help.github.com/categories/releases/) (which depend on tags).

This is particularly important for new versions of the standard, as each version's documentation should point to specific versions of its extensions. For more information, see [pinning extensions](../standard/technical/deployment#pin-extensions).

[Community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions), on the other hand, are externally maintained and not associated to each version of the standard.

## Reporting issues on extensions

[Issues](https://help.github.com/articles/about-issues/) on [*core* extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) should be reported to the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions). Collecting issues in one place gives each more visibility and therefore a higher likelihood of being closed. It also helps to identify related issues across different extensions. When creating an issue, indicate the extension in the issue's title, e.g. *extension name: issue title*.

To report issues on [community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions), refer to each extension's documentation.

If the issue is with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), report it on the [`standard` repository](https://github.com/open-contracting/standard) and add the `Focus - Extensions` label to the issue.

## Tools

* [standard_extension_template](https://github.com/open-contracting/standard_extension_template), as described above
* [extension_creator](https://github.com/open-contracting/extension_creator) is a web interface for modifying any of OCDS' schema files and either generating the corresponding patch file or the complete corresponding extension.
* [extension_registry](https://github.com/open-contracting/extension_registry), as described above
