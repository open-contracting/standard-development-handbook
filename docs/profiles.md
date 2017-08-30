# OCDS Profiles

e.g. [http://standard.open-contracting.org/profiles/ppp/latest/en/](http://standard.open-contracting.org/profiles/ppp/latest/en/)

## Updating the schema and codelists

The PPP profile is built by patching the core OCDS schema and codelists with various extensions.

### Pulling in updated extensions

To include an updated extension in the PPP profile build:

1. Create a new release in Github for the version of the extension to be included in the PPP profile build (see [worked example](../deployment/standard-live/#to-pin-extensions-worked-example))
1. Update the extension.json for the extension in the [ppp branch](https://github.com/open-contracting/extension_registry/tree/ppp) of the extension registry so that the `url` key points to the release created in step 1
1. Run [apply-extensions.py](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py)
1. If the updated extension introduces or removes codelists from the extension, update [codelists.md](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

### Updating the base schema and codelist

To update the base schema and codelists that the PPP extension is built on:

1. Replace the contents of the [base-codelists](https://github.com/open-contracting/public-private-partnerships/tree/master/schema/base-codelists) folder with the new base codelists
1. Replace [base-release-schema.json](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/base-release-schema.json) with the new base schema
1. Run [apply-extensions.py](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py)
1. If the updated base schema and codelists introduce and remove codelists, update [codelists.md](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

### Adding a new extension

To include a new extension in the PPP profile build:

1. Create a new release in Github for the version of the extension to be included in the PPP profile build (see [worked example](../deployment/standard-live/#pinning-extensions-worked-example))
1. Add an entry for the extension in the [ppp branch](https://github.com/open-contracting/extension_registry/tree/ppp) of the extension registry so that the `url` key points to the release created in step 1
1. Update the `extensions_to_merge` list in [apply-extensions.py](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py) to include the slug for the extension (specified in the entry in the extension registry)
1. Run [apply-extensions.py](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py)
1. If the new extension introduces or removes codelists, update [codelists.md](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

*Note: Currently apply-extensions.py will only work wih extensions hosted under the open-contracting Github organization.*

## Travis

Each branch of the [public-private-partnerships](https://github.com/open-contracting/public-private-partnerships) repo gets automatically built to:

`http://standard.open-contracting.org/profiles/ppp/<branch>/en/`

## Copying live deploy into place

(See the [servers](deployment/servers) page for more info on how our servers are set up.)

```bash
VER=1.0            # (for example)
DATE=$(date +%F)   # or YYYY-MM-DD to match the release date on dev3
                   # (see ${VER}/en/index.html)
SEQ=1              # To deploy again on the same day, increment to 2 etc
PROFILE=ppp        # (for example)

# Copy from dev3 to your local box
scp -r \
  root@dev3.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/${VER} \
  ${VER}-${DATE}-${SEQ}

# Copy from your local box to live2
scp -r \
  ${VER}-${DATE}-${SEQ} \
  root@live2.default.opendataservices.uk0.bigv.io:/home/ocds-docs/web/profiles/${PROFILE}/

# Symlink the version number
ssh root@live2.default.opendataservices.uk0.bigv.io \
  "rm /home/ocds-docs/web/profiles/${PROFILE}/${VER}; ln -sf ${VER}-${DATE}-${SEQ} /home/ocds-docs/web/profiles/${PROFILE}/${VER}"
```
