# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch versions, as well as non-normative versions.

For changes to documentation only (no schema changes), start from [Translate and release](#translate-and-release).

For changes to the theme only, start from [Build and deploy](#build-and-deploy).

## Schemas and extensions

### 1. Review extensions

#### Review pull requests and recent changes

For each *core* extension, [spell check](../spellcheck), [run Markdownlint](../../../coding#linting), and ensure it:

* [Passes its tests on Travis](https://github.com/open-contracting/standard-maintenance-scripts/blob/master/badges.md#extensions)
* Matches the description in [Creating extensions](../../../extensions#creating-extensions) regarding license, issues and `README.md`
* [Has wiki disabled, default branch protected, and topics set](https://github.com/open-contracting/standard-maintenance-scripts#change-github-repository-configuration)

The following Rake tasks from [standard-maintenance-scripts](https://github.com/open-contracting/standard-maintenance-scripts) will report or correct issues with licenses, issues, `README.md`, wikis, branches, and topics:

```bash
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

```bash
bundle exec rake release:review_extensions
```

#### Create new versions of core extensions

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Each OCDS version refers to a specific version of each [core extension](http://standard.open-contracting.org/latest/en/extensions/#core-extensions). The [governance process](http://standard.open-contracting.org/latest/en/support/governance/#versions) will establish whether to create a new version of a core extension for this OCDS version.

For each *core* extension for which to create a new version:

1. From the list of releases, click *Draft a new release*
1. In *Tag version*, enter the version number in *vmajor.minor.patch* format, e.g. `v1.1.1`
1. Enter a summary of changes, e.g. "Typo fixes", and click *Publish release*

Instead of navigating the website, use this Rake task, which will use the extension's changelog as the release message:

```bash
bundle exec rake release:release_extensions REF=v1.1.1 REPOS=repo1,repo2
```

If you make a mistake, you can undo the release with:

```bash
bundle exec rake release:undo_release_extensions REF=v1.1.1 REPOS=repo1,repo2
```

Then, add the new releases to the [extension registry](https://github.com/open-contracting/extension_registry). To quickly generate the content of `extension_versions.csv` with the new releases of core extensions, run:

```bash
bundle exec rake registry_extension_versions
```

### 2. Perform periodic updates, if appropriate

#### Update currency codelist

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Before each release, and at least once a year (because ISO4217 is updated [at least once a year](https://github.com/open-contracting/standard/pull/607#issuecomment-339093306)), run:

```shell
python standard/schema/utils/fetch_currency_codelist.py
```

### 3. Update version numbers, validation schema and changelog

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

In `standard/docs/en/conf.py`, update `release` to e.g. `1.1.1` and update `version` if appropriate.

Update the *major__minor__patch* version number:

```bash
find . \( -name '*.json' -or -name '*.md' -or -name '*.po' \) -exec sed -i "" 's/1__1__3/1__1__4/g' \{\} \;
```

Update `versioned-release-validation-schema.json` to match `release-schema.json`:

```shell
python standard/schema/utils/make_validation_schema.py
```

Update `meta-schema.json` to match `meta-schema-patch.json`:

```shell
python standard/schema/utils/make_metaschema.py
```

Update the standard's [changelog](http://standard.open-contracting.org/latest/en/schema/changelog/#changelog) with a summary of the changes to core extensions.

### 4. Integrate extensions

Pull some files from extensions into the standard:

```bash
python standard/schema/utils/fetch_core_extensions.py
```

### 5. Set up a development instance of CoVE (OCDS Validator)

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Set up a development instance of CoVE using the new schema, and run tests against it.

## Merge and release

### 1. Push and pull updated translations

1. [Push strings to translate to Transifex](../../translation/technical#push-strings-to-translate-to-transifex).
1. Check all strings are [translated](../../translation/using_transifex#translator) and [reviewed](../../translation/using_transifex#reviewer) in supported translations, e.g. [French](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#fr/$/) and [Spanish](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/$/) for OCDS 1.1.
1. For any resources with untranslated or unreviewed strings, follow the [translation process](../../translation/workflow).
1. Check the [warnings](../../translation/using_transifex#view-translations-with-warnings) on Transifex, and correct translated text if necessary.
1. [Pull supported translations from Transifex](../../translation/technical#pull-translations-from-transifex).
1. Check the [issues](../../translation/using_transifex#view-translations-with-issues) on Transifex, and correct source and `.po` files if necessary.
1. If `.po` files were corrected, you may need to [forcefully push supported translations to Transifex](../../translation/technical#push-translations-to-transifex).
1. Create a pull request for the updated translation files.
1. [Test the translations on the build of the pull request](../../translation/technical#test-translations).

### 2. Merge the development branch onto the live branch

The dev working branch should be merged into the relevant live branch, e.g. merge `1.1-dev` onto `1.1`. Do this in the GitHub interface, or locally with a no-ff merge (so that we get a merge commit to record when the live branch was updated). If required, this may happen by first merging a patch dev branch (`1.1.1-dev`) into the minor (`1.1-dev`) dev branch, and then merging onwards into the live branch (`1.1`).

### 3. Create a tagged release

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Create a tagged release named e.g. `git tag -a 1__1__0 -m '1.1.0 release.'` and push the tag with `git push --tags`

## Build and deploy

### 1. Build on Travis

[Merging the development branch onto the live branch](#merge-the-development-branch) will trigger a [build](../build) on Travis. For changes to the theme, hit rebuild on the previous build of the live branch.

Travis copies the built documentation to the development server. You can preview the documentation, e.g. for OCDS 1.1,
<http://ocds-standard.dev3.default.opendataservices.uk0.bigv.io/1.1/en/> is the development deploy for <http://standard.open-contracting.org/1.1/en/>.

### 2. Copy the files to the live server

(See the [servers](../../servers) page for more information on how our servers are set up.)

Each deploy has its own unique folder on the live server (including the date and a sequence number). The bare version number is then symlinked. This makes it easy to roll back deploys.

Set some variables:

```bash
VER=1.1            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3 (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2, etc.
BASEDIR=/home/ocds-docs/web/
```

Copy from dev server to your local box:

```bash
scp -r root@dev3.default.opendataservices.uk0.bigv.io:${BASEDIR}${VER} ${VER}-${DATE}-${SEQ}
```

Copy from your local box to the live server:

```bash
scp -r ${VER}-${DATE}-${SEQ} root@live2.default.opendataservices.uk0.bigv.io:${BASEDIR}
```

Symlink the version number:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm ${BASEDIR}${VER}; ln -sf ${VER}-${DATE}-${SEQ} ${BASEDIR}${VER}"
```

If a new language is supported, edit `http://standard.open-contracting.org/robots.txt`

### 3. Copy the schema into place

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Copy the JSON from the schema directory of the build to `/home/ocds-docs/web/schema/[release_tag]` on the live server, e.g. for 1.1.1:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io
mkdir /home/ocds-docs/web/schema/1__1__1/
cp -r /home/ocds-docs/web/1.1/en/*.json /home/ocds-docs/web/schema/1__1__1/
```

The JSON files are then visible at <http://standard.open-contracting.org/schema/1__1__1/>.

### 4. Update the "latest" branch

If the build should also appear at [/latest/](http://standard.open-contracting.org/latest/), update the `latest` branch on GitHub to point to the same commit, then repeat [Build on Travis](#build-on-travis) and [Copy the files to the live server](#copy-the-files-to-the-live-server) with `VER=latest`.

Doing a build is necessary because some URLs are updated with the branch name (e.g. links in the schema).

### 5. Update the deployment repository

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

* [For major, minor or patch versions, edit the version switcher](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/version-options.html)
* [For major and minor versions, edit `live_versions` in the Apache configuration file](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L16)
* For major and minor versions, edit the [dev](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_dev.html) and [old](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_old.html) banners

### 6. Update the live CoVE deployment (OCDS Validator)

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Update the live CoVE deployment to use the new schema.

## FAQ

### How can I find out what the standard looked like at 1.0?

To find the latest (patch) version of a minor release, look at the contents of the branch named with that version.

### How can I find out what the standard looked like at 1.1.0?

To find a patch release, look at the contents of the tree tagged with that version.
