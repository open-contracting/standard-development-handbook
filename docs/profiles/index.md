# OCDS Profiles

## Public Private Partnerships

### Repository

The repository for [this profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/public-private-partnerships).

### Versioning

Currently the PPP profile doesn't have a version number.

### Branch naming

The working copy of the PPP profile is on the `master` branch.

A `live` branch will be created to reflect the version which is deployed for the launch of the PPP profile.

## Schema and codelists

The PPP profile is built by patching the core OCDS schema and codelists with various extensions by running `apply-extensions.py`.

The list of extensions with which to patch the core standard is defined in the `extensions_to_merge` list in `apply-extensions.py`.

The compiled schema and codelists are located in the [`schema`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema) and [`compiledCodelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/compiledCodelists) directories respectively.

### Pulling in a new or updated extension

To include a new or updated extension in the profile build:

1. Create a new release in GitHub for the version of the extension to be included in the profile build (see [worked example](../standard/deployment#pinning-extensions-worked-example)).
1. In the [ppp branch](https://github.com/open-contracting/extension_registry/tree/ppp) of the extension registry, if the extension is new, add an entry for it or otherwise update its `extension.json`, so that the `url` key points to the release created in step 1.
1. If the extension is new, update the `extensions_to_merge` list in [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py) to include the slug for the extension (specified in the entry in the extension registry).
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the extension introduces or removes codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

```eval_rst
  .. note::
    Currently, `apply-extensions.py` will only work with extensions hosted under the open-contracting GitHub organization.
```

### Updating the base schema and codelist

To update the base schema and codelists that the profile is built on:

1. Replace the contents of the [`base-codelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema/base-codelists) directory with the new base codelists.
1. Replace [`base-release-schema.json`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/base-release-schema.json) with the new base schema.
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the updated base schema and codelists introduce and remove codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

## Translation

A Spanish translation of the profile is maintained using Transifex.

## Travis

Each branch of the [public-private-partnerships](https://github.com/open-contracting/public-private-partnerships) repo gets automatically built to:

`http://standard.open-contracting.org/profiles/ppp/<branch>/en/`

## Copying live deploy into place

(See the [servers](../systems/servers) page for more info on how our servers are set up.)

Set some variables:

```bash
VER=1.0            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
PROFILE=ppp        # (for example)
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
