# Terminology

In order to use key terms consistently across the standard documentation and OCP communication in general, terminology is managed according to a light-weight process that ensures quality.

![Terminology process overview](https://www.lucidchart.com/invitations/accept/2eee45ed-5e62-4636-9a44-24b4414f273f)

## 1. Proposition and validation
## Tools overview

### Google spreadsheet

The Google spreadsheet is divided in sheets.

The first sheet is the English sheet. It holds the source terms, their class, their definition, and any other field necessary to caracterize the source terms and help the translators. Only the people who validate the new terms and those who work on the definitions can edit this sheet.

All subsequent sheets are dedicated to the translations. One sheet is created for each language variant (fr_FR, es_ES, es_UY, etc.). The first columns of these sheets are imported from the English sheets, with all the fields. New terms added in the English sheet are automatically visible in the translation sheets. For each translation sheet, only the translators and the proofreaders can edit the sheet.

All the sheets are publicly readable.

### GitHub

GitHub is used as the source of truth for OCP terminology. The terms, definitions and translations that are pushed to the repository have been previously spellchecked.

The benefit of using Git is that it neatly tracks the changes made to the files and it incorporates a convenvient issue tracker to track the progression of certain tasks.

## Roles overview

### Author

The author writes English content for the OCP.

They inform the terminologist when they have written chunks of content about new concepts.

### Terminologist

The terminologist recognizes what is a term and what isn't. They may also be an author.

### Subject matter expert

The subject matter expert (SME) is an expert in the domain of application of the terms.

If they work on the definitions, they are fluent in English.

If they translate the terms, they are fluent in the target language. They understand written English and are able to find terms in their language that equivalent to the source English terms.

### Language owner

The language owner oversees the translations of one or more variations of a language. They are the reference contacts for the subject matter experts (SMEs) who translate the terms.

They are fluent practioners of the language they oversee.

### Proofreader

The proofreader ensures that the translated terms and their comments are well written and understandable.

They are a native speaker of the target language.

The proofreader may be a language owner, but not necessarily.



When new content is added to the documentation and new concepts are introduced in the standard, new terms may need to be translated.

**Reminder:** a term is a word or group of words that must be used and translated consistently to ensure a good understanding and usage of the content. Synonyms of terms must consequently be banned. Expressions that are not terms are called *generic* expressions.

| #   | Step name   | Description                                                                                                                 | Tool               |
| --- | ----------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| 1   | Proposition | The author of new or updated text prepares a list of expressions (words or groups of words) that they consider to be terms. | GitHub issue       |
| 2   | Validation  | A terminologist validates that the proposed expressions are actually terms.                                                 | GitHub issue       |
| 3   | Inclusion   | The new terms are added in the working document, checking for duplicates.                                                   | Google spreadsheet |


## 2. Definition

When new terms are added to the working document, subject matter experts (SME) in the source language are notified, and write a definition for each term. The definitions must be bound to the context of the source documents, and not general.

Using other terms of the glossary in the definitions is a good practice and helps contextualize the terms.

If the definition is copied from an existing publication, please add the URL or reference at the end of the definition.

| #   | Step name  | Description                                                                           | Tool               |
| --- | ---------- | ------------------------------------------------------------------------------------- | ------------------ |
| 1   | Definition | The source language SME writes a definition for each term, or copies an existing one. | Google spreadsheet |



## 3. Translation

When the definition of the new terms are ready, subject matter experts (SME) in the other languages are notified. They only translate terms to their native language.

The SME may add a comment in the `comment_xx-XX` column to explain the choice of the term. The comment must be written in the target language.

The SME pays attention to the definition given for the term, as it may narrow down the meaning and lead to a translation that is more specific than the usual translation of the source term.


| #   | Step name   | Description                                                                           | Tool               |
| --- | ----------- | ------------------------------------------------------------------------------------- | ------------------ |
| 1   | Translation | The SME translates the terms to the target language and adds comments when necessary. | Google spreadsheet |

## 4. Proofreading and editing

When the SME is done translating the new terms (or trying to), the proofreader enforces a list of rules to maintain the readability of the terms and the associated comments.

| #   | Step name    | Description                                                                                                               | Tool               |
| --- | ------------ | ------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| 6   | Translations | The proofreader checks the translations are spelled correctly and written in lower case (proper nouns and acronyms excepted). | Google spreadsheet |
| 7   | Comments     | The proofreader makes sure the comments are spelled correctly and written as full sentences in sentence case                  | Google spreadsheet |


## 5. Publication

Once the translations are proofread and edited, *someone* downloads the working document as a CSV file and replaces the previous file in the GitHub repository.

Then, they upload the same CSV to Transifex.

Steps 1 and 2 of this stage can be scripted.

| #   | Step name                 | Description                                                                      | Tool               |
| --- | ------------------------- | -------------------------------------------------------------------------------- | ------------------ |
| 1   | CSV download              | File > Download as... > Comma-separated values                                   | Google spreadsheet |
| 2   | Github commit             | The CSV file replaces the previous one for the selected language and is commited | Git                |
| 3   | Transifex glossary update | The CSV file is uploaded to Transifex glossary, deleting the previous entries    | Transifex          |
