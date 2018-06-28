# Profiles

Profiles are adaptations of OCDS to suit the disclosure requirements and user needs of a particular sector, type of contracting process and/or legal framework.

Profiles typically bring together a number of extensions to meet these requirements and, in some rare cases, can also make fundamental changes to the OCDS schema which would not be permitted in a core or community extension.

Profiles are built to their own documentation micro-sites which may include:

* The full profile schema
* A mapping between the disclosure requirements and/or legal framework and the schema
* Worked examples
* Introductory material and implementation guidance

Profiles are, in many ways, similar to the [standard](../standard) itself, including [building](../standard/technical/build) and [translating](../standard/translation) the documentation. Differences are noted on this page.

New profiles can be created using [this template](https://github.com/open-contracting/standard_profile_template).

```eval_rst
.. toctree::
   :maxdepth: 2
   :glob:

   deployment
   integrations
   ppp
```

## Branches

The development version of a profile is on the `master` branch, and the live version is on the `live` branch.

## Translation

Translations of profiles are maintained using Transifex, same as the [standard's translations](../standard/translation).

### Copying translations from the standard to a profile

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
