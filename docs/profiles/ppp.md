# Public Private Partnerships

[This profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/public-private-partnerships). It is [deployed](http://standard.open-contracting.org/profiles/ppp/) with the standard documentation. It was previously deployed to <http://ocds-for-ppps.readthedocs.io/>, which uses meta refresh to redirect to the current deployment.

## Update OCDS Show for PPPs

The profile contains a copy of OCDS Show for PPPs. To update it:

```shell
make update_ocds_show
```

## Combine extensions' schema and codelists

The PPP profile patches the core OCDS schema and codelists with extensions, including itself. The list of extensions is in `schema/apply-extensions.py`. The combined patches and codelists are located in the [`schema`](https://github.com/open-contracting/public-private-partnerships/tree/master/schema) and [`compiledCodelists`](https://github.com/open-contracting/public-private-partnerships/tree/master/compiledCodelists) directories and are calculated by running:

```shell
make clean_dist
python schema/apply-extensions.py
```

### Update the base schema and codelist files

```
make update_base_files
```

Then combine extensions' schema and codelists with the new base files.

If the new base files introduce and remove codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

### Pull in a new or updated extension

To include a new or updated extension in a build:

1. Create a new release in GitHub for the version of the extension to be included in the profile build (see [worked example](../standard/technical/deployment#pin-extensions)).
1. Update the [extension registry](https://github.com/open-contracting/extension_registry).
1. Update `extension_versions` in [`conf.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/conf.py).
1. Run [`apply-extensions.py`](https://github.com/open-contracting/public-private-partnerships/blob/master/schema/apply-extensions.py).
1. If the extension introduces or removes codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.
