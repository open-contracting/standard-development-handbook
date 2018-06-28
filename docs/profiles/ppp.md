# Public Private Partnerships

[This profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting/public-private-partnerships). It is [deployed](http://standard.open-contracting.org/profiles/ppp/) with the standard documentation. It was previously deployed to <http://ocds-for-ppps.readthedocs.io/>, which uses meta refresh to redirect to the current deployment.

## Development tasks

### Update OCDS Show for PPPs

The profile contains a copy of OCDS Show for PPPs. To update it:

```shell
make update_ocds_show
```

### Change extensions or version of OCDS

If extensions or OCDS introduce or remove codelists, update [`codelists.md`](https://github.com/open-contracting/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

## Translation

See the generic profile [translation documentation](../translation).

For reference:

* The translations of the consolidated extension's codelists are used by `bids.md`.
* The translations of the patched OCDS's codelists are used by `codelists.md` and `documents.md`.
* The translation of the patched OCDS's release schema is used by `framework.md`, `documents.md` and `schema.md`
