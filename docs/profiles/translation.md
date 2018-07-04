# Translation

See the standard's page for [Translation](../../standard/translation).

## Copying translations from the standard to a profile

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

## Technical implementation of translation

See the standard's page for [Technical implementation of translation](../../standard/translation/implementation).

* `.babel_codelists` indicates the codelist CSV files in the consolidated extension and the patched OCDS (`schema/*/codelists/*.csv`) from which to extract strings to translate.
* `.babel_schema` indicates the JSON Schema files in the consolidated extension and the patched OCDS (`schema/*/*-schema.json`) from which to extract strings to translate.
* `conf.py` calls `translate_codelists` to translate the codelist files from `schema/profile/codelists` to `docs/extensions/codelists_translated`, and from `schema/patched/codelists` to `docs/_static/patched/codelists`.
* `conf.py` calls `translate_schema` to translate the schema files from `schema/patched` to `docs/_static/patched`.
