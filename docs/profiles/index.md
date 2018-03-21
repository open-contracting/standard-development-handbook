# Profiles

New profiles can be created using [profile_template](https://github.com/open-contracting/profile_template).

### Branches

The stable version of a profile is on the `live` branch, and the development version is on the `master` branch.

## Translation

Translations of profiles are maintained using Transifex.

### Copying translations from the standard to a profile

There is often overlap between a profile and the standard, e.g. all the text from the unextended schema.

We can copy translations using `pretranslate` from `translate-toolkit` (replace `profile`):

```bash
git clone https://github.com/open-contracting/standard.git
git clone https://github.com/open-contracting/profile.git

# Merge all the standard's translations for one language into a single file.
msgcat standard/standard/docs/locale/es/LC_MESSAGES/{*.po,*/*.po} > profile/es.po

cd profile

# Extract POT files from JSON, CSV and Markdown files.
make extract

cd locale/es/LC_MESSAGES

# Copy the translations.
for f in *.po */*.po; do
  pretranslate --tm ../../../es.po -t $f ../../../build/locale/${f}t $f;
done
```

## Travis

Each branch of a profile's repository is automatically built to:

`http://standard.open-contracting.org/profiles/<root>/<branch>/en/`

## Copying live deploy into place

See the [servers](../systems/servers) page for more info on how our servers are set up.

Set some variables (change `PROFILE`):

```bash
VER=master         # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
PROFILE=root       # (for example)
```

Copy from dev server to your local box:

```bash
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/${VER} \
  ${VER}-${DATE}-${SEQ}
```

Copy from your local box to the live server:

```bash
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/
```

Symlink the version number:

```bash
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/profiles/${PROFILE}/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/profiles/${PROFILE}/${VER}"
```

## Public Private Partnerships

[This profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/public-private-partnerships).

### Building the documentation

The steps are similar to [those for the standard](../standard/technical/build). Differences are:

* Build the documentation in `docs/_build/dirhtml` with: `cd docs; make -e SPHINXOPTS="-D language='en'" dirhtml`
* The profile has no tests

### Translation

The steps are similar to [those for the standard](../standard/translation/technical). Differences are:

* Update the `.tx/config` file with: `sphinx-intl update-txconfig-resources --transifex-project-name ocds-for-ppps --pot-dir build/locale --locale-dir locale`
* When running `pybabel extract`, prefix the schema and codelists `.pot` files with `ppp-`

### Schema and codelists

The PPP profile is built by patching the core OCDS schema and codelists with various extensions by running `apply-extensions.py`.

The list of extensions with which to patch the core standard is defined in the `extensions_to_merge` list in `apply-extensions.py`.

The compiled schema and codelists are located in the [`schema`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema) and [`compiledCodelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/compiledCodelists) directories respectively.

#### Pulling in a new or updated extension

To include a new or updated extension in a profile build:

1. Create a new release in GitHub for the version of the extension to be included in the profile build (see [worked example](../standard/technical/deployment#pin-extensions)).
1. In the [ppp branch](https://github.com/open-contracting/extension_registry/tree/ppp) of the extension registry, if the extension is new, add an entry for it or otherwise update its `extension.json`, so that the `url` key points to the release created in step 1.
1. If the extension is new, update the `extensions_to_merge` list in [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py) to include the slug for the extension (specified in the entry in the extension registry).
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the extension introduces or removes codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

```eval_rst
  .. note::
    Currently, `apply-extensions.py` will only work with extensions hosted under the open-contracting GitHub organization.
```

#### Updating the base schema and codelist

To update the base schema and codelists that a profile is built on:

1. Replace the contents of the [`base-codelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema/base-codelists) directory with the new base codelists.
1. Replace [`base-release-schema.json`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/base-release-schema.json) with the new base schema.
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the updated base schema and codelists introduce and remove codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.
