# Terminology

In order to use key terms consistently across the standard documentation and OCP communication in general, terminology is managed according to a light-weight process that ensures quality.

![Terminology process overview](https://www.lucidchart.com/publicSegments/view/888e3ab4-65bd-497e-b0fa-f2e91515672e/image.png)

## Tools overview

### Google spreadsheet

The Google spreadsheet is divided in sheets. Each term is identified by an ID to enable the reconciliation of the terms across languages and enable the management of homographs (different terms that have the same spelling).

All the sheets are publicly readable and can be commented by anyone.

#### Source

The Source sheet is edited by the terminologist and the SMEs and proofreaders in the source language. It has the following columns:

- **ID**: the ID of a term never changes. When a new term is added, it takes the next available ID number.
- **Term**: the term, in its canonical form (lower case, singular, infinitive)
- **Definition**: the definition of the term **within the scope of OCDS documentation**. To improve the usability and efficiency of the glossary, please try to use other terms of the glossary in the definition.
- **Comment**: any remark the terminologist may want to add to help translating this term

#### Languages (es, fr, etc.)

The sheet of a language is edited by the SMEs and the proofreaders. It has the following columns:

- **ID**: the ID of the term. It enables the synchronization with the Source sheet and connects all the translations of the term.
- **Term**, **Definition**, **Comment**: the content of these fields is automatically imported from the Source sheet. Once one of these values is modified in the Source sheet, it can take up to a minute for the values to be updated in all the sheets.
- **Translation**: the equivalent of the source term in the target language, in its canonical form (lower case, singular, infinitive). Like two synonyms in the same language, the translation of a term may have a slightly different meaning or usage. If so, please highlight this difference in the definition and optionnally in the comment field.
- **Definition**: the definition of the term in the target language. This is not necessarily a translation of the source definition. To improve the usability and efficiency of the glossary, please try to use other terms of the glossary in the definition.
- **Comment**: any remark the SME may want to add to explain the choice or the definition of the term in the target language.

#### Language variants (es-MX, es-GT, fr-BE, etc.)

The sheet of a language variant is edited by the SMEs and the proofreaders. It has the following columns:

- Same as languages
- **Varies from language?**: this cell is automated and it can have the following values:
    - **no** if the term in the language variant and the base language are the same
    - **yes => term** if the term in the language variant differs from the one in the base language
    - **empty** if either the base language or the language variant doesn't have a term yet


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

## Process

### 1. Proposal, review, inclusion

When new content is added to the documentation and new concepts are introduced in the standard, new terms may need to be translated.

**Reminder:** a term is a word or group of words that must be used and translated consistently to ensure a good understanding and usage of the content. Synonyms of terms should consequently be avoided. Expressions that are not terms are called *generic* expressions.

| #   | Step name   | Description                                                                                                                 | Tool               |
| --- | ----------- | --------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| 1   | Proposition | The author of new or updated text prepares a list of expressions (words or groups of words) that they consider to be terms. | GitHub issue       |
| 2   | Validation  | A terminologist validates that the proposed expressions are actually terms.                                                 | GitHub issue       |
| 3   | Inclusion   | The new terms are added in the working document, checking for duplicates.                                                   | Google spreadsheet |


### 2. Definition

When new terms are added to the working document, subject matter experts (SME) in the source language are notified, and write a definition for each term. The definitions must be bound to the context of the source documents, and not general.

Using other terms of the glossary in the definitions is a good practice and helps contextualize the terms.

If the definition is copied from an existing publication, please add the URL or reference at the end of the definition.

| #   | Step name  | Description                                                                           | Tool               |
| --- | ---------- | ------------------------------------------------------------------------------------- | ------------------ |
| 4   | Definition | The source language SME writes a definition for each term, or copies an existing one. | Google spreadsheet |



### 3. Translation

When the definition of the new terms are ready, subject matter experts (SME) in the other languages are notified. They only translate terms to their native language.

The SME may add a comment in the `comment_xx-XX` column to explain the choice of the term. The comment must be written in the target language.

The SME pays attention to the definition given for the term, as it may narrow down the meaning and lead to a translation that is more specific than the usual translation of the source term.


| #   | Step name   | Description                                                                           | Tool               |
| --- | ----------- | ------------------------------------------------------------------------------------- | ------------------ |
| 5   | Translation | The SME translates the terms to the target language and adds comments when necessary. | Google spreadsheet |

### 4. Proofreading and editing

When the SME is done translating the new terms (or trying to), the proofreader enforces a list of rules to maintain the readability of the terms and the associated comments.

| #   | Step name    | Description                                                                                                               | Tool               |
| --- | ------------ | ------------------------------------------------------------------------------------------------------------------------- | ------------------ |
| 6   | Translations | The proofreader checks the translations are spelled correctly and written in lower case (proper nouns and acronyms excepted). | Google spreadsheet |
| 7   | Comments     | The proofreader makes sure the comments are spelled correctly and written as full sentences in sentence case                  | Google spreadsheet |


### 5. Publication

Once the translations are proofread and edited, *someone* downloads the working document as a CSV file and replaces the previous file in the GitHub repository.

Then, they upload the same CSV to Transifex.

Steps 1 and 2 of this stage can be scripted.

| #   | Step name                 | Description                                                                      | Tool               |
| --- | ------------------------- | -------------------------------------------------------------------------------- | ------------------ |
| 8   | CSV download              | File > Download as... > Comma-separated values                                   | Google spreadsheet |
| 9   | GitHub commit             | The CSV file replaces the previous one for the selected language and is commited | Git                |
| 10  | Transifex glossary update | The CSV file is uploaded to Transifex glossary, deleting the previous entries    | Transifex          |

### 6. Management tasks

Certain tasks are not directly related to the production of the glossary, but are necessary for good coordination:

- The author informs the terminologist that a new batch of terms is ready for review.
- *Someone* informs the translators that new terms should be translated.
- The language owners manage the permissions for each sheet to enable the translators to translate.
- The language owners inform *someone* that a certain batch of terms is translated, proofread and edited, ready to be pushed to the GitHub repository.
- *Someone* informs *someone* that batch of terms has been pushed to GitHub, ready to be published to Transifex.
