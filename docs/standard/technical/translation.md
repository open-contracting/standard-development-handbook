# Translation

This page documents only the steps required to include translations in a documentation build. See the [full translation process](../translation).

## Configuring Transifex

The first time you use Transifex, run (replacing `USERNAME` and `PASSWORD`):

```shell
sphinx-intl create-transifexrc --transifex-username USERNAME --transifex-password PASSWORD
```

For major and minor versions:

* [Create a new Transifex project](https://www.transifex.com/OpenDataServices/) named e.g. `open-contracting-standard-1-1`
* Empty the `.tx/config` file:

        tx init

For major, minor and patch versions:

* [Build the documentation](build). It is normal to see "inconsistent term references in translated message" warnings.
* Update the `.tx/config` file (replacing the Transifex project name):

        sphinx-intl update-txconfig-resources --transifex-project-name open-contracting-standard-1-1 --pot-dir build/locale --locale-dir standard/docs/locale

Whenever documentation pages are renamed, added or removed, you must build the documentation and update the `.tx/config` file.

## Translating text

To push untranslated text to Transifex, run:

```shell
tx push -s
```

To forcefully pull all translated text from Transifex, run:

```shell
tx pull -f -a
```

To forcefully pull specific translations from Transifex, run:

```shell
tx pull -f -l es,fr
```

Then, [build the documentation](build) again.

If text is translated locally by editing `.po` files, the translations can be pushed to Transifex. After pushing, check that the translation progress on Transifex is minimally affected:

```shell
tx push -f -t -l es,fr --no-interactive
```

**This will overwrite any new translations made on Transifex since the last time they were pulled.** To avoid losing translations made on Transifex, pull translations before applying your changes, re-building the documentation and pushing new translations. If you made a mistake, checkout a clean branch of the standard, re-build the documentation and push old translations.

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
