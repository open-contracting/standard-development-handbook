# Extensions

## Creating extensions

To create a new extension, you should use the [standard extension template](https://github.com/open-contracting/standard_extension_template), which following the [core OCDS schema](https://github.com/open-contracting/standard/tree/master/standard/schema) includes the following files:

* release-schema.json
* release-package-schema.json
* record-package-schema.json

Extensions must include at least one schema file. In most cases, the extension will have a _release-schema.json_ with the minimal changes required to patch the schema, although there may be more marginal user cases requiring metadata patches for _release-package-schema.json_ and/or _record-package-schema.json_. Empty schema files should not be included in the extension.

Under the hood, OCDS extensions use JSON merge patch to apply changes to the target schema. To know more, see [JSON merge patch documentation](https://tools.ietf.org/html/rfc7396).

Repositories for [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) should have issue submissions disable by default and should direct developers to the [OCDS extension issues repository](https://github.com/open-contracting/ocds-extensions) to file issues. Best practice is to add that information to the _README.md_ file in every core extension using the following template:

```none

### Reporting issues

By default, issues are disabled for individual OCDS core extensions. Instead, there is an [ocds extension repository](https://github.com/open-contracting/ocds-extensions) to gather issues for all extensions in a single place.

If you have an issue to report, please submit it there. Make sure you indicate the appropriate extension following this format in the title: **_extension_name: issue title_**.

```

For [community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions) there is no specific requirements regarding issue management.

## Naming extensions

Names for extensions should conform to the following pattern:

`ocds_[name]_extension`

`[name]` should be based on a JSON Pointer fragment for the name of the primary field or the primary object being added, or both if necessary. The idea is that the name should be a good indication of which part of the schema is being targeted, thus contributing to self-documenting the extension.

When naming an extension, camel case (_camelCase_) should be replace with lowercase plus underscores (_camel_case_).

## Extension descriptions

Here are some guidelines for writing the text for the mandatory field `"description"` in _extension.json_ :

* There is no maximum length for the description, but you should try to keep it concise. In any case, do not sacrifice clarity for the sake of brevity.
* Refer to the part(s) of the schema the extension is modifying.
* Do not include in the description the development status of the extension (e.g. _draft_). If you need to add current status, do so in a _README_ file, it will be much more visible and therefore less prone to be forgotten and not updated.
* Avoid descriptions that simply duplicate or paraphrase the extension name.

For example, for [ocds_performance_failures_extension](https://github.com/open-contracting/ocds_performance_failures) , this wouldn't be a good description:

  > _"An extension covering performance failures in OCDS."_

The actual description in the extension is much better:

  > _"This extension introduces a performance failures array to the implementation section of OCDS, based on the performance failures reporting table defined in the framework for disclosure in PPPs."_

## Extension codelists

As in the code standard repository, in the [standard extension template](https://github.com/open-contracting/standard_extension_template) there is also a [codelists folder](https://github.com/open-contracting/standard_extension_template/tree/master/codelists) to store extension-specific codelists.

Codelists are CSV files with camel case names , e.g. _contractStatus.csv_. Be aware that a codelist in your extension using the same name of an existing codelist in the standard repository will override the existing codelist.

## Versioning Extensions

The standard [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) are currently versioned using [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) via the [releases feature in GitHub](https://help.github.com/categories/releases/) (which builds on Git tags).

This is particularly important for new releases and deployments of OCDS, as each release of the standard should point to specific versions of each extensions. For more information, see [freeze extensions](../deployment/standard-live#freeze-extensions) in the standard deployment section.

[Community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions), on the other hand, are externally maintained and not pinned to releases of the standard.

N.B. The mechanism for versioning extensions both 'internally' (addressing changes within the extension during the _same_ standard release cycle) and 'externally' (with reference to _different_ standard versions) is likely to change in the future. Take a look at this [GitHub issue](https://github.com/open-contracting/extension_registry/issues/47) in the [extension registry](https://github.com/open-contracting/extension_registry) repo for more information on this topic.

## Tools

### Extension creator

The [Extension creator](https://github.com/open-contracting/extension_creator) is a GUI that allows you to modify any of the schema files and get the corresponding patch file for the extension.

The tool will create a zip file to download, containing the patch schema file plus the _extension.json_ file with the name and description given by you.

### Extension tester

Another useful tool to help creating extensions is the [Extension tester](https://github.com/open-contracting/extension_tester), which provides a simple way of testing your extensions on your local machine.

## Extension registry

The [Extensions registry](https://github.com/open-contracting/extension_registry) is the place where extensions are recorded in order to be included in the OCDS documentation.

Every extension recorded in the registry must have an _entry.json_ file valid against the [entry-schema.json](https://github.com/open-contracting/extension_registry/blob/master/entry-schema.json).

[compile.py](https://github.com/open-contracting/extension_registry/blob/master/compile.py) needs to be run for the docs to pick up
new extensions or changes to existing ones.

`python compile.py` will generate two non version-controlled files (_extensions.json_ and _extension.js_) which are the reference files that OCDS needs to build the documentation on extensions.

## Extension issues

[GitHub issues](https://help.github.com/articles/about-issues/) for [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) should be submitted to the [OCDS extension issues repository](https://github.com/open-contracting/ocds-extensions), which is dedicated to gather issues for all core extensions.

You should submit extension-specific issues to that repository. Collecting all issues in a single place gives much more visibility to them and therefore a higher likelihood of getting closed soon. Also, it helps to identify related issues across extensions.

When creating an issue, make sure you indicate the appropriate standard extension following the title format **_extension_name: issue title_**.

If you think you have identified a problem with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), you may consider opening an issue in the [core standard repository](https://github.com/open-contracting/standard) pinning the `Extensions` tag to that issue.

For [community extension](http://standard.open-contracting.org/latest/en/extensions/#community-extensions) issues refer to each extension specific documentation.


