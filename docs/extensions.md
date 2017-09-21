# Extensions

## Creating extensions

To create a new extension, it is recommended to use the [standard extension template](https://github.com/open-contracting/standard_extension_template).

Under the hood, OCDS extensions use JSON merge patch to apply changes to the target schema. To know more, see [JSON merge patch documentation](https://tools.ietf.org/html/rfc7396).

Repositories for [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) should have issue submissions disable by default and should direct developers to the [OCDS extension issues repository](https://github.com/open-contracting/ocds-extensions) to file issues. Best practice is to add that information to the _README.md_ file in every core extension using the following template:

### Reporting issues

Report issues for this extension in the [ocds-extensions repository](https://github.com/open-contracting/ocds-extensions/issues), putting the extension's name in the issue's title.

For [community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions) there is no specific requirements regarding issue management.

## Versioning Extensions

The standard [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) are currently versioned using [Git tags](https://git-scm.com/book/en/v2/Git-Basics-Tagging) via the [releases feature in GitHub](https://help.github.com/categories/releases/) (which builds on Git tags).

This is particularly important for new releases and deployments of OCDS, as each release of the standard should point to specific versions of each extensions. For more information, see [freeze extensions](../deployment/standard-live#freeze-extensions) in the standard deployment section.

[Community extensions](http://standard.open-contracting.org/latest/en/extensions/#community-extensions), on the other hand, are externally maintained and not pinned to releases of the standard.

N.B. The mechanism for versioning extensions both 'internally' (addressing changes within the extension during the _same_ standard release cycle) and 'externally' (with reference to _different_ standard versions) is likely to change in the future. Take a look at this [GitHub issue](https://github.com/open-contracting/extension_registry/issues/47) in the [extension registry](https://github.com/open-contracting/extension_registry) repo for more information on this topic.

## Tools

### Extension creator

The [Extension creator](https://github.com/open-contracting/extension_creator) is a GUI that allows you to modify any of the schema files and get the corresponding patch file for the extension.

### Extension tester

The [Extension tester](https://github.com/open-contracting/extension_tester) provides a simple way to test your extensions on your local machine.

## Extension registry

The [Extensions registry](https://github.com/open-contracting/extension_registry) is the place where extensions are recorded in order to be included in the OCDS documentation.

## Extension issues

[GitHub issues](https://help.github.com/articles/about-issues/) for [core extensions](http://standard.open-contracting.org/latest/en/extensions/#core-extensions) should be submitted to the [OCDS extension issues repository](https://github.com/open-contracting/ocds-extensions), which is dedicated to gather issues for all core extensions.

You should submit extension-specific issues to that repository. Collecting all issues in a single place gives much more visibility to them and therefore a higher likelihood of getting closed soon. Also, it helps to identify related issues across extensions.

When creating an issue, make sure you indicate the appropriate standard extension following the title format **_extension_name: issue title_**.

If you think you have identified a problem with extensions as a whole (e.g. there is something wrong in the way the standard deals with extensions), you may consider opening an issue in the [core standard repository](https://github.com/open-contracting/standard) pinning the `Extensions` tag to that issue.

For [community extension](http://standard.open-contracting.org/latest/en/extensions/#community-extensions) issues refer to each extension specific documentation.
