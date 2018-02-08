# Deployment

This section describes the steps involved in deploying an updated version of the standard to become the live version.

This process is used for major, minor and patch versions, as well as non-normative versions.

For changes to documentation only (no schema changes), start from [Translate and release](#translate-and-release).

For changes to the theme only, start from [Build and deploy](#build-and-deploy).

## Schemas and extensions

### 1. Review extensions

#### Review pull requests and recent changes

For each *core* extension, [spell check](http://ocds-standard-development-handbook.readthedocs.io/en/latest/standard/technical/spellcheck/), [run Markdownlint](http://ocds-standard-development-handbook.readthedocs.io/en/latest/coding/#linting), and ensure it:

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

#### Create new releases of core extensions

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Each release of the standard should pin to specific versions of each [core extension](http://standard.open-contracting.org/latest/en/extensions/#core-extensions). Community extensions are not pinned.

For each *core* extension:

1. From the list of releases, click *Draft a new release*
1. In *Tag version*, enter the OCDS version in *vmajor.minor.patch* format, e.g. `v1.1.1`
1. In *Release title*, enter a title, e.g. "Fixed version for OCDS 1.1.1"
1. Enter a summary of changes, e.g. "Typo fixes", and click *Publish release*

Instead of navigating the website, run this Rake task, which will use the extension's changelog as the release message and e.g. "Fixed version for OCDS 1.1.1" as the release title:

```bash
bundle exec rake release:release_extensions REF=v1.1.1
```

Then, create a new branch of the extension registry to point to the new releases of core extensions.

### 2. Perform periodic updates, if appropriate

#### Update currency codelist

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Before each release, and at least once a year, run `python standard/schema/utils/fetch_currency_codelist.py`. ISO4217 is updated [at least once a year](https://github.com/open-contracting/standard/pull/607#issuecomment-339093306).

### 3. Update version numbers, validation schema and changelog

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Update `release` in `standard/docs/en/conf.py` to e.g. `1.1.1`. If the new extension registry branch you created doesn't correspond to `release` (i.e. `v1.1.1`), update `extension_registry_git_ref`.

Update the `"id"` at the top of each JSON Schema file, and any `"$ref"` using these IDs, to match the *major__minor__patch* version number:

```bash
python standard/schema/utils/update_schema_ids.py
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

1. Run `tx push -s` to push source files to Transifex.
1. Check all strings are translated and reviewed in supported translations, e.g. for OCDS 1.1: [French](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#fr/$/), [Spanish](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/translate/#es/$/)
1. For any resources with untranslated or unreviewed strings, follow the [translation process](../translation#translation-workflow).
1. Run `tx pull -f -l es,fr` to pull updated translation files to the repository.
1. Commit the updated translation files to the repository.

### 2. Merge the development branch

The dev working branch should be merged into the relevant live branch, e.g. merge `1.1-dev` onto `1.1`. Do this in the GitHub interface, or locally with a no-ff merge (so that we get a merge commit to record when the live branch was updated). If required, this may happen by first merging a patch dev branch into the dev branch for a major or minor version, and then merging onwards into the live branch.

### 3. Create a tagged release

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

Create a tagged release named e.g. `1__1__0`

## Build and deploy

### 1. Build on Travis

[Merge the development branch](#merge-the-development-branch) will trigger a [build](../build) on Travis. For changes to the theme, hit rebuild on the previous build for the relevant live branch.

Travis copies the built docs to the dev server, you can check they look okay there. e.g. for 1.1:
<http://ocds-standard.dev3.default.opendataservices.uk0.bigv.io/1.1/en/> or <http://standard.open-contracting.org/1.1/en/>.

### 2. Copy the files to the live server

(See the [servers](../../servers) page for more info on how our servers are set up.)

Each deploy has its own unique folder on the live server (including the date and a sequence number). The bare version number is then symlinked. This makes it easy to roll back the live docs.

Set some variables:

```bash
VER=1.1            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
```

Copy from dev server to your local box:

```bash
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/${VER} \
  ${VER}-${DATE}-${SEQ}
```

Copy from your local box to the live server:

```bash
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/
```

Symlink the version number:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/${VER}"
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

If the build should also appear at [/latest/](http://standard.open-contracting.org/latest/), then update the `latest` branch on GitHub to point to the same commit. Wait for the Travis build, then repeat [Copy the files to the live server](#copy-the-files-to-the-live-server) with `VER=latest`.

Doing a build is necessary because some URLs are updated with the branch name (e.g. links in the schema).

### 5. Update the Apache config

```eval_rst
  .. note::
    You can skip this step if you are not releasing a new major, minor or patch version.
```

For a new live version, you will need to edit:

* [live_versions in the Apache config](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/apache/ocds-docs-live.conf#L16)
* [version switcher](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/version-options.html)
* [dev](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_dev.html) and [old](https://github.com/OpenDataServices/opendataservices-deploy/blob/master/salt/ocds-docs/includes/banner_old.html) banners

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
