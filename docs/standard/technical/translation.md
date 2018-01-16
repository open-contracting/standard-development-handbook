# Translation

This page documents only the steps required to include translations in a documentation build. See the [full translation process](../translation).

## Configuring Transifex

The first time you use Transifex, run (replacing `USERNAME` and `PASSWORD`):

```shell
sphinx-intl create-transifexrc --transifex-username USERNAME --transifex-password PASSWORD
```

When a new major/minor version of the documentation text is ready:

* [Build the documentation](build)
* [Create a Transifex project](https://www.transifex.com/OpenDataServices/) named e.g. `open-contracting-standard-x.y`
* Empty the `.tx/config` file:

    cat /dev/null > .tx/config

* Update the `.tx/config` file (replacing the Transifex project name):

    sphinx-intl update-txconfig-resources --transifex-project-name open-contracting-standard-x.y --pot-dir build/locale --locale-dir standard/docs/locale

The last step must also be run whenever documentation pages are renamed, added or removed.

## Translating text

To push untranslated text to Transifex, run:

```shell
tx push -s
```

To pull all translated text from Transifex, run:

```shell
tx pull -f -a
```

To pull one translation from Transifex, run:

```shell
tx pull -f -l fr
```

Then, [build the documentation](build) again.

If text is translated locally by editing `.po` files, the translations can be pushed to Transifex. Note that this will overwrite any new translations made on Transifex since the last time they were pulled:

```shell
tx push -t --skip
```

The [theme needs to be translated separately](https://github.com/open-contracting/standard_theme#translations).

## Testing translations

```eval_rst
  .. todo::
    Provide steps to carry out for testing translations.
```

## Review translated codelists

Translated codelists are temporarily stored in `standard/schema/translated_codelists` during the [build](build) process. To translated a codelist to one language, run:

```shell
cd standard
CODELIST_LANG=es_MX python schema/utils/translate_codelists.py
```

To combine the CSV files for review, run:

```shell
for i in *.csv; do printf "\n\n$i,,,\n\n"; cat $i; done > ../all_codelists.csv
```
