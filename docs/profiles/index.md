# Profiles

Profiles are, in many ways, similar to the [standard](../standard) itself, including [building](../standard/technical/build) and [translating](../standard/translation) the documentation. Differences are noted on this page.

New profiles can be created using [this template](https://github.com/open-contracting/standard_profile_template).

### Branches

The development version of a profile is on the `master` branch, and the live version is on the `live` branch.

## Translation

Translations of profiles are maintained using Transifex, same as the [standard's translations](../standard/translation).

### Copying translations from the standard to a profile

There is often overlap between a profile and the standard, e.g. all the text from the unextended schema.

We can copy translations using `pretranslate` from `translate-toolkit` (replace `PROFILE`):

```bash
git clone https://github.com/open-contracting/standard.git
git clone https://github.com/open-contracting/PROFILE.git

# Merge all the standard's translations for one language into a single file.
msgcat standard/standard/docs/locale/es/LC_MESSAGES/{*.po,*/*.po} > PROFILE/es.po

cd PROFILE

# Extract POT files from JSON, CSV and Markdown files.
make extract

# Copy the translations.
for f in locale/es/LC_MESSAGES/{*.po,*/*.po}; do
  pretranslate --tm es.po -t $f build/locale/${f}t $f;
done
```

## Travis

Each branch of a profile's repository is automatically built to:

`http://standard.open-contracting.org/profiles/{root}/{branch}/en/`

## Copying live deploy into place

See the [servers](../systems/servers) page for more info on how our servers are set up.

Set some variables (change the value of `PROFILE`):

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

[This profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/public-private-partnerships). It is [deployed](http://standard.open-contracting.org/profiles/ppp/) with the standard documentation. It was previously deployed to <http://ocds-for-ppps.readthedocs.io/>, which uses meta refresh to redirect to the current deployment.

### Update OCDS Show for PPPs

The profile contains a copy of OCDS Show for PPPs. To update it:

```shell
make update_ocds_show
```

### Combine extensions' schema and codelists

The PPP profile patches the core OCDS schema and codelists with extensions, including itself. The list of extensions is in `schema/apply-extensions.py`. The combined patches and codelists are located in the [`schema`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema) and [`compiledCodelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/compiledCodelists) directories and are calculated by running:

```shell
make clean_dist
python schema/apply-extensions.py
```

#### Update the base schema and codelist files

```
make update_base_files
```

Then combine extensions' schema and codelists with the new base files.

If the new base files introduce and remove codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

#### Pull in a new or updated extension

To include a new or updated extension in a build:

1. Create a new release in GitHub for the version of the extension to be included in the profile build (see [worked example](../standard/technical/deployment#pin-extensions)).
1. In the [ppp branch](https://github.com/open-contracting/extension_registry/tree/ppp) of the extension registry, if the extension is new, add an entry for it or otherwise update its `extension.json`, so that the `url` key points to the release created in step 1.
1. If the extension is new, update the `extensions_to_merge` list in [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py) to include the slug for the extension (specified in the entry in the extension registry).
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the extension introduces or removes codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

```eval_rst
  .. note::
    Currently, `apply-extensions.py` will only work with extensions hosted under the open-contracting GitHub organization.
```
