# Using Transifex

## Translation glossary

A translation glossary is [available](https://www.transifex.com/OpenDataServices/open-contracting-standard-1-1/glossary/en/) (change the language code at the end of the URL to view the glossary in different languages). It can also be accessed from within the translation editor.

The glossary contains key terms that must be used consistently.

In our translation process, we encourage translators to:

1. Populate the glossary with suggested translations of its terms
1. Validate the translations with the nominated reviewer
1. Translate the rest of the documentation

## Tasks

### Controlling access permissions

Read Transifex's documentation on [inviting collaborators](https://docs.transifex.com/teams/inviting-collaborators/) and [understanding user roles](https://docs.transifex.com/teams/understanding-user-roles). For more documentation, see [Getting Started as a Localization Manager](https://docs.transifex.com/getting-started/getting-started-as-a-manager).

### Counting untranslated words

The dashboard of a translation project reports the number of *strings* to translate, but translators must know the number of *words* to translate in order to estimate the time and cost. To get the number of words:

1. Open the translation project
1. Scroll to the list of languages and click "Translate" for a language
1. Click "All resources" at the bottom of the screen
1. Click "# untranslated" at the top of the screen
1. Check the box at the right of the search bar
1. See the number of words at the right of the screen

### How-to

```eval_rst
  .. todo::
    Add guidance on how to use Transifex. CRM issue #3034.
```

From the translation interface, type `?` to see a list of shortcuts.

### What not to translate

Some titles and descriptions of codes are copied from external sources and should be translated by those sources, not OCDS. These are tagged as `should_be_translated_upstream` and indicated by a small tag icon.
