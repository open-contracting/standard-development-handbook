# Translation technical processes

This page documents only the technical steps to push and pull translations from Transifex and to build translated schema, codelists and documentation. See the [full translation process](translation).

You should only perform the tasks on this page once the source files are frozen; the documentation should be ready to deploy except for translations, i.e. you completed the [Schemas and extensions](../technical/deployment#schemas-and-extensions) part of the deployment process.

## Configure Transifex

The first time you use Transifex, run (replace `USERNAME` and `PASSWORD`):

```shell
sphinx-intl create-transifexrc --transifex-username USERNAME --transifex-password PASSWORD
```

For major and minor versions:

* [Create a Transifex project](https://www.transifex.com/OpenDataServices/), named e.g. `open-contracting-standard-1-1`
* Update `TRANSIFEX_PROJECT` in `include/config.mk`
* Empty the `.tx/config` file:

        rm -f .tx/config
        sphinx-intl create-txconfig

For major, minor and patch versions:

* [Build the documentation](build). There should be no warnings, except "inconsistent term references in translated message" warnings. :issue:`139`
* Update the `.tx/config` file with `make update_txconfig`

Whenever documentation pages are renamed, added or removed, you must build the documentation and update the `.tx/config` file.

## Push and pull translations from Transifex

To **push** source files to Transifex, run `make push` or `tx push -s`

To **push** specific resources among source files to Transifex (replace the Transifex project name):

```shell
tx push -s -r open-contracting-standard-1-1.codelists open-contracting-standard-1-1.schema
```

To forcefully **pull** *supported* translations from Transifex, run `make pull` or `tx pull -f -l es,fr`

To forcefully **pull** *all* translations from Transifex:

```shell
tx pull -f -a
```

Then, [build the documentation](build) again with the new translations.

If text is translated locally by editing `.po` or `.pot` files, the translations can be pushed to Transifex, **after building the documentation**. **This will overwrite any new translations made on Transifex since the last time they were pulled.** Run `make force_push_all` or `tx push -s -t -f -l es,fr --no-interactive`

After pushing, check that the translation progress on Transifex is minimally affected. To avoid losing translations made on Transifex, pull translations before applying your changes, re-building the documentation and pushing new translations. If you made a mistake, checkout a clean branch of the standard, re-build the documentation and push old translations.

## Test translations

Pull requests are built and accessible at `http://standard.open-contracting.org/BRANCH/`. Translations of Markdown pages using Sphinx directives should be checked in particular:

* `http://standard.open-contracting.org/BRANCH/en/getting_started/` uses `jsoninclude`
* `http://standard.open-contracting.org/BRANCH/es/schema/reference/` uses `jsonschema`
* `http://standard.open-contracting.org/BRANCH/es/schema/release/` has a Docson widget
* `http://standard.open-contracting.org/BRANCH/es/schema/codelists/` uses `csv-table-no-translate`
* `http://standard.open-contracting.org/BRANCH/es/extensions/` uses `extensionselectortable`
* `http://standard.open-contracting.org/BRANCH/es/extensions/bids/` uses `extensiontable`
* `http://standard.open-contracting.org/BRANCH/es/extensions/party_details/` uses `extensionlist`

## Review translated codelists

Translated codelists are stored in language directories under `build/codelists` during the build process.

To stack a list of CSV files for review, you can do:

```bash
for i in *.csv; do printf "\n\n$i,,,\n\n"; cat $i; done > ../all_codelists.csv
```
