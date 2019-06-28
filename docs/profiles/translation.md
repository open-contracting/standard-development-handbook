# Translation

See the standard's page for [Translation](../../../standard/translation/index).

## Copying translations from the standard to a profile

There is often overlap between a profile and the standard, e.g. all the text from the unextended schema.

These instructions are similar to others in [ocds-extensions-translations](https://github.com/open-contracting/ocds-extensions-translations#populate-initial-translations) (using the fish shell on macOS).

1. Install `translate-toolkit`:

        brew install translate-toolkit

1. Install `python-Levenshtein`:

        eval (brew --prefix translate-toolkit)/libexec/bin/pip install python-Levenshtein

1. Set environment variables:

        set lang language
        set wip path/to/profile/directory

1. Change into the `standard` directory
1. Prepare a compendium from the `standard` repository:

        git checkout 1.1
        msgcat --use-first standard/docs/locale/$lang/**.po > $wip/$lang-standard.po
        git checkout 1.1-dev

1. Change into the `ocds-extensions-translations` directory
1. Prepare a compendium from the profile's extensions, for example, for OCDS for PPPs:

        for version in bids/v1.1.4 budget/master budget_project/master charges/master documentation_details/master finance/master location/v1.1.4 metrics/master milestone_documents/v1.1.4 performance_failures/master process_title/v1.1.4 qualification/master requirements/master risk_allocation/master shareholders/master signatories/master tariffs/master transaction_milestones/master ppp/master
          msgcat --use-first locale/$lang/LC_MESSAGES/$version/**.po > $lang-(echo $version | tr '/' '-').po
        end
        msgcat --use-first (ls $lang-*.po) > $wip/$lang-extensions.po
        rm -f $lang-*.po

1. Change into the profile's directory
1. Prepare a compendium from the profile's repository, and merge it:

        if [ -d locale/$lang/LC_MESSAGES ]
          msgcat --use-first $lang-standard.po $lang-extensions.po locale/$lang/**.po > $lang.po
        else
          msgcat --use-first $lang-standard.po $lang-extensions.po > $lang.po
        end

1. Create the POT files:

        make extract

1. Re-create the PO files:

        rm -rf locale/$lang/LC_MESSAGES
        sphinx-intl update -p build/locale -d locale -l $lang

1. Pre-populate the PO files:

        cd locale/$lang/LC_MESSAGES
        for f in **.po
          pretranslate --nofuzzymatching -t ../../../$lang.po ../../../build/locale/{$f}t $f
        end
        cd ../../..

1. Count untranslated messages:

        pocount --incomplete locale/$lang/LC_MESSAGES

1. Clean up:

        rm -f $lang-standard.po $lang-extensions.po $lang.po

## Technical implementation of translation

See the standard's page for [Technical implementation of translation](../../../standard/translation/implementation).

* `babel_ocds_codelist.cfg` indicates the codelist CSV files in the consolidated extension and the patched OCDS (`schema/*/codelists/*.csv`) from which to extract strings to translate.
* `babel_ocds_schema.cfg` indicates the JSON Schema files in the consolidated extension and the patched OCDS (`schema/*/*-schema.json`) from which to extract strings to translate.
* `conf.py` calls `translate` to translate the JSON Schema files and codelist CSV files from `schema/profile` to `build/<lang>`, and from `schema/patched` to `docs/_static/patched`.
