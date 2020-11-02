# Public Private Partnerships

[This profile](https://standard.open-contracting.org/profiles/ppp/latest/en/) is developed and maintained by the Open Contracting Partnership on [GitHub](https://github.com/open-contracting-extensions/public-private-partnerships). It is [deployed](https://standard.open-contracting.org/profiles/ppp/) with the standard documentation. It was previously deployed to <https://ocds-for-ppps.readthedocs.io/>, which uses meta refresh to redirect to the current deployment.

## Development tasks

### Update examples

The profile contains example files from OCDS Show for PPPs. To update them:

```shell
make update_examples
```

### Change extensions or version of OCDS

See the generic profile [build documentation](technical/build).

If extensions or OCDS introduce or remove codelists, update [`codelists.md`](https://github.com/open-contracting-extensions/public-private-partnerships/blob/master/docs/reference/codelists.md) accordingly.

To find codelists to add or remove, run (in Bash):

```shell
diff -u <(ls -1 schema/profile/codelists | sed 's/^[+-]//' | sort | uniq) <(grep :file: docs/reference/codelists.md | cut -d'/' -f 5 | sort)
```

## Translation

See the generic profile [translation documentation](translation).

For reference:

* The translations of the patched OCDS's codelists are used by `codelists.md` and `documents.md`.
* The translation of the patched OCDS's release schema is used by `framework.md`, `documents.md` and `schema.md`
