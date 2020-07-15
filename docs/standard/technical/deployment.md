# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch versions, as well as non-normative versions.

For changes to the documentation only (no schema changes), start from [Merge and release](#merge-and-release).

For changes to the theme only, start from [Build and deploy](#build-and-deploy).

To add a community translation, [follow these instructions](../translation/technical.html#add-a-community-translation).

## Schemas and extensions

### 1. Review extensions

#### Review pull requests and recent changes

For each *core* extension, [spell check](spellcheck), [run Markdownlint](../../coding.html#linting), and ensure it:

* [Passes its tests](https://github.com/open-contracting/standard-maintenance-scripts/blob/master/badges.md#extensions)
* Matches the description in [Creating extensions](../../extensions.html#creating-extensions) regarding license, issues and `README.md`
* [Has wiki disabled, default branch protected, and topics set](https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration)

The following Rake tasks from [standard-maintenance-scripts](https://github.com/open-contracting/standard-maintenance-scripts) will report or correct issues with licenses, issues, `README.md`, wikis, branches, and topics:

```shell
bundle exec rake repos:licenses
bundle exec rake repos:readmes
bundle exec rake fix:lint_repos
bundle exec rake fix:protect_branches
bundle exec rake fix:set_topics
```

Then, for each *core* extension, review the commits since the last release:

1. Open its homepage on GitHub
1. Open its releases (under the repository title and description from its homepage)
1. Decide whether to merge its open pull requests
1. View the commits since the last release (under the release's heading) and consider any substantive changes, i.e. not simple typo or documentation updates

Instead of navigating the website, run this Rake task to get links to pull requests and comparison URLs:

```shell
bundle exec rake release:review_extensions
```

#### Create new versions of core extensions

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

Each OCDS version refers to a specific version of each [core extension](https://standard.open-contracting.org/latest/en/extensions/#core-extensions). The [governance process](https://standard.open-contracting.org/latest/en/support/governance/#versions) will establish whether to create a new version of a core extension for this OCDS version.

For each *core* extension for which to create a new version:

1. From the list of releases, click *Draft a new release*
1. In *Tag version*, enter the version number in *vmajor.minor.patch* format, e.g. `v1.1.1`
1. Enter a summary of changes, e.g. "Typo fixes", and click *Publish release*

Instead of navigating the website, use this Rake task, which will use the extension's changelog as the release message:

```shell
bundle exec rake release:release_extensions REF=v1.1.1 REPOS=repo1,repo2
```

If you make a mistake, you can undo the release with:

```shell
bundle exec rake release:undo_release_extensions REF=v1.1.1 REPOS=repo1,repo2
```

Then, add the new releases to the [extension registry](https://github.com/open-contracting/extension_registry). To quickly generate the content of `extension_versions.csv` with the new releases of core extensions, run:

```shell
bundle exec rake registry:extension_versions
```

### 2. Perform periodic updates, if appropriate

#### Update currency codelist

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

Before each release, and at least once a year (because ISO4217 is updated [at least once a year](https://github.com/open-contracting/standard/pull/607#issuecomment-339093306)), run:

```shell
python utils/fetch_currency_codelist.py
```

### 3. Update version numbers, versioned release schema and changelog

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

In `docs/conf.py`, update `release` to e.g. `1.1.1` and update `version` if appropriate.

Update the *major__minor__patch* version number:

```shell
find . \( -name '*.json' -or -name '*.md' -or -name '*.po' \) -exec sed -i "" 's/1__1__3/1__1__4/g' \{\} \;
```

Update `versioned-release-validation-schema.json` and `dereferenced-release-schema.json` to match `release-schema.json`:

```shell
python utils/make_versioned_release_schema.py
python utils/make_dereferenced_release_schema.py
```

Update `meta-schema.json` to match `meta-schema-patch.json`:

```shell
python utils/make_metaschema.py
```

Update the standard's [changelog](https://standard.open-contracting.org/latest/en/schema/changelog/#changelog) with a summary of the changes to core extensions.

### 4. Set up a development instance of CoVE (OCDS Data Review Tool)

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

Set up a development instance of CoVE using the new schema, and run tests against it.

## Merge and release

### 1. Push and pull updated translations

1. [Push strings to translate to Transifex](../translation/technical.html#push-strings-to-translate-to-transifex).
1. Check all strings are [translated](../translation/using_transifex.html#translator) and [reviewed](../translation/using_transifex.html#reviewer) in supported translations, e.g. [French](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#fr/$/) and [Spanish](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/$/) for OCDS 1.1.
1. For any resources with untranslated or unreviewed strings, follow the [translation process](../translation/workflow).
1. Check the [warnings](../translation/using_transifex.html#view-translations-with-warnings) on Transifex, and correct translated text if necessary.
1. [Pull supported translations from Transifex](../translation/technical.html#pull-translations-from-transifex).
1. Check the [issues](../translation/using_transifex.html#view-translations-with-issues) on Transifex, and correct source and `.po` files if necessary.
1. If `.po` files were corrected, you may need to [forcefully push supported translations to Transifex](../translation/technical.html#push-translations-to-transifex).
1. Create a pull request for the updated translation files.
1. [Test the translations on the build of the pull request](../translation/technical.html#test-translations).

### 2. Merge the development branch onto the live branch

Create a pull request to merge the development branch into its corresponding live branch, e.g. `1.1-dev` into `1.1`. This might happen by first merging a patch dev branch (`1.1.1-dev`) into the minor dev branch (`1.1-dev`), and then merging into the live branch (`1.1`).

If the live branch is for the latest version of the documentation, then create a pull request to merge it into the `latest` branch.

### 3. Create a tagged release

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

Create a tagged release named e.g. `git tag -a 1__1__0 -m '1.1.0 release.'` and push the tag with `git push --tags`

## Build and deploy

### 1. Build on continuous integration

[Merging the development branch onto the live branch](#merge-the-development-branch) will trigger a [build](build). For changes to the theme, rebuild the previous build of the live branch.

The built documentation is copied to the staging server. You can preview the documentation. For example, for OCDS 1.1,
<http://staging.standard.open-contracting.org/1.1/en/> is the staging version for <https://standard.open-contracting.org/1.1/en/>.

### 2. Release the documentation

See the [deploy repository's documentation](https://ocdsdeploy.readthedocs.io/en/latest/deploy/docs.html#publish-released-documentation).

### 3. Update the Data Review Tool

```eval_rst
.. note::
   You can skip this step if you are not releasing a new major, minor or patch version.
```

#### Update the CoVE library

This is the lib-cove-ocds repository for OCDS, and lib-cove-oc4ids for OC4IDS.

* Update the URL paths in [config.py](https://github.com/open-contracting/lib-cove-ocds/blob/master/libcoveocds/config.py)
* Make sure all tests pass
* [Release a new version](https://ocp-software-handbook.readthedocs.io/en/latest/python/packages.html#release-process)

#### Update and deploy the Data Review Tool

This is the cove-ocds repository for OCDS, and cove-oc4ids for OC4IDS.

* Upgrade the requirements to use the new version of the CoVE library

```shell
pip-compile -P libcoveocds; pip-compile requirements_dev.in
```

* Update the URL paths in [settings.py](https://github.com/OpenDataServices/cove/blob/master/cove_ocds/settings.py) (*only in cove-ocds*)
* Make sure all tests pass
* [Deploy the app](https://ocdsdeploy.readthedocs.io/en/latest/deploy/deploy.html)

#### Update any other tools that use the CoVE library

Make sure other tools that use lib-cove-ocds (like Kingfisher) are updated to use the new version.

Many tools will use the default options from the library, and these tools will start using the new version of the schema straight away. But if the tool overrides those options with its own options, the tool's own options may need changing.

## FAQ

### How can I find out what the standard looked like at 1.0?

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

### How can I find out what the standard looked like at 1.1.0?

To find a patch release, look at the contents of the tree tagged with that version.
