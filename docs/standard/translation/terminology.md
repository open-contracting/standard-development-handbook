# Terminology

In order to use key terms consistently across the standard documentation and OCP communication in general, terminology is managed according to a light-weight process that ensures quality.

![Terminology process overview](https://www.lucidchart.com/publicSegments/view/888e3ab4-65bd-497e-b0fa-f2e91515672e/image.png)

<!-- https://www.lucidchart.com/documents/edit/3d906148-5ed8-41a4-b48d-8d3ec3aed1d4 -->

## Tools

### Google spreadsheet

[The Google spreadsheet](https://docs.google.com/spreadsheets/d/1PvlA2WWtP9KJpnkhuYGx5ExHmHwwvaA54VX62piF86k/edit) is divided in sheets. Each term is identified by an ID to enable the reconciliation of the terms across languages and enable the management of homographs (different terms that have the same spelling).

All the sheets are publicly readable and can be commented by anyone.

#### Source

The Source sheet is edited by the terminologist and the SMEs and proofreaders in the source language. It has the following columns:

- **ID**: the ID of a term never changes. When a new term is added, it takes the next available ID number.
- **Term**: the term, in its canonical form (lower case, singular, infinitive)
- **POS**: the part of speech (Noun, Verb, Adjective)
- **Domain**: the subject matter domain (procurement, technical)
- **Definition**: the definition of the term **within the scope of OCDS documentation**. To improve the usability and efficiency of the glossary, please try to use other terms of the glossary in the definition. The definition cell is a good place to give concise examples.
- **Note**: any remark the terminologist may want to add to help translating this term or a URL to information about the term.

#### Base languages (es, fr, etc.)

The sheet of a language is edited by the SMEs and the proofreaders. It has the following columns:

- Same as source
- **xx**: the equivalent of the source term in the target language, in its canonical form (lower case, singular, infinitive). Like two synonyms in the same language, the translation of a term may have a slightly different meaning or usage. If so, please highlight this difference in the definition and optionally in the comment field.
- **Definition_xx**: the definition of the term in the target language. This is not necessarily a translation of the source definition. To improve the usability and efficiency of the glossary, please try to use other terms of the glossary in the definition.
- **Note_xx**: any remark the SME may want to add to explain the choice or the definition of the term in the target language.

#### Language variants (es-MX, es-GT, fr-BE, etc.)

The sheet of a language variant is edited by the SMEs and the proofreaders. It has the following columns:

- Same as base language, renaming **xx** to **Translation_xx** and removing **Note** and **Note_xx**
- **xx_XX**: the equivalent of the source term in the target locale, in its canonical form (lower case, singular, infinitive).
- **Note_xx_XX**: any remark the SME may want to add to explain the choice of the term in the target locale.
- **Varies from xx?**: this cell is automated and it can have the following values:
    - **no** if the term in the language variant and the base language are the same
    - **yes => term** if the term in the language variant differs from the one in the base language
    - **empty** if either the base language or the language variant doesn't have a term yet

### GitHub

GitHub is used as the source of truth for OCP terminology. The terms, definitions and translations that are pushed to the repository have been previously spellchecked.

The benefit of using Git is that it neatly tracks the changes made to the files and it incorporates a convenient issue tracker to track the progression of certain tasks.

### Transifex

[Transifex](https://www.transifex.com/OpenDataServices/public/) is the tool currently used by the Open Contracting Partnership to manage the translation of their content. One of its features is a glossary that enables translators to access the translated terms when translating.

## Roles

### Author

The author writes English content for the OCP.

They inform the terminologist when they have written chunks of content about new concepts.

### Terminologist

The terminologist recognizes what is a term and what isn't. They may also be an author.

### Subject matter expert

The subject matter expert (SME) is an expert in the domain of application of the terms.

If they work on the definitions, they are fluent in English.

If they translate the terms, they are fluent in the target language. They understand written English and are able to find terms in their language that equivalent to the source English terms.

### Coordinator

The coordinator oversees the translation of the terms of base languages and language variants. They are the reference contact for the subject matter experts (SMEs) who translate the terms and for the proofreaders.

### Proofreader

The proofreader ensures that the translated terms and their comments are well written and understandable.

They are a native speaker of the target language.

The proofreader may be a coordinator, but not necessarily.

### Publisher

The publisher gathers the data from the spreadsheet and makes sure it gets published.

## Process

### 1. Proposal, review, inclusion

When new content is added to the documentation and new concepts are introduced in the standard, new terms may need to be translated.

**Reminder:** a term is a word or group of words that must be used and translated consistently to ensure a good understanding and usage of the content. Synonyms of terms should consequently be avoided. Expressions that are not terms are called *generic* expressions.

```eval_rst
=== =========== =========================================================================================================================== ==================
#   Step name   Description                                                                                                                 Tool
=== =========== =========================================================================================================================== ==================
1   Proposal    The author of new or updated text prepares a list of expressions (words or groups of words) that they consider to be terms. GitHub issue
2   Review      A terminologist validates that the proposed expressions are actually terms.                                                 GitHub issue
3   Inclusion   The new terms are added in the working document, checking for duplicates.                                                   Google spreadsheet
=== =========== =========================================================================================================================== ==================
```

### 2. Definition

When new terms are added to the working document, subject matter experts (SME) in the source language are notified, and write a definition for each term. The definitions must be bound to the context of the source documents, and not general.

Using other terms of the glossary in the definitions is a good practice and helps contextualize the terms.

If the definition is copied from an existing publication, please add the URL or reference at the end of the definition.

```eval_rst
=== ========== ===================================================================================== ==================
#   Step name  Description                                                                           Tool
=== ========== ===================================================================================== ==================
4   Definition The source language SME writes a definition for each term, or copies an existing one. Google spreadsheet
=== ========== ===================================================================================== ==================
```

### 3. Translation

When the definition of the new terms are ready, subject matter experts (SME) in the other languages are notified. They only translate terms to their native language.

The SME may add a comment in the `comment_xx-XX` column to explain the choice of the term. The comment must be written in the target language.

The SME pays attention to the definition given for the term, as it may narrow down the meaning and lead to a translation that is more specific than the usual translation of the source term.

```eval_rst
=== =========== ===================================================================================== ==================
#   Step name   Description                                                                           Tool
=== =========== ===================================================================================== ==================
5   Translation The SME translates the terms to the target language and adds comments when necessary. Google spreadsheet
=== =========== ===================================================================================== ==================
```

### 4. Proofreading and editing

When the SME is done translating the new terms (or trying to), the proofreader enforces a list of rules to maintain the readability of the terms and the associated comments.

```eval_rst
=== ============ ============================================================================================================================= ==================
#   Step name    Description                                                                                                                   Tool
=== ============ ============================================================================================================================= ==================
6   Translations The proofreader checks the translations are spelled correctly and written in lower case (proper nouns and acronyms excepted). Google spreadsheet
7   Comments     The proofreader makes sure the comments are spelled correctly and written as full sentences in sentence case                  Google spreadsheet
=== ============ ============================================================================================================================= ==================
```

### 5. Publication

Once the translations are proofread and edited, the publisher downloads the working document as a CSV file and replaces the previous file in the GitHub repository.

Then, they upload the same CSV to Transifex.

Steps 1 and 2 of this stage can be scripted.

```eval_rst
=== ========================= ================================================================================= ==================
#   Step name                 Description                                                                       Tool
=== ========================= ================================================================================= ==================
8   CSV download              File > Download as... > Comma-separated values                                    Google spreadsheet
9   GitHub commit             The CSV file replaces the previous one for the selected language and is committed Git
10  Transifex glossary update The CSV file is uploaded to Transifex glossary, deleting the previous entries     Transifex
=== ========================= ================================================================================= ==================
```

### 6. Management tasks

Certain tasks are not directly related to the production of the glossary, but are necessary for good coordination:

- Authors propose candidate terms to Terminologists to review and include.
- Terminologists inform Coordinators of new terms to be translated.
- Coordinators inform SMEs of new terms to translate.
- Coordinators inform Proofreaders of translated terms to proofread.
- Coordinators manage the permissions of each sheet and give SMEs and Proofreaders the right to edit any relevant sheets.
- Coordinators inform Publishers that terms are translated and proofread, ready to be pushed to the GitHub repository and Transifex.

At all stages, every person involved uses ranges or list of term IDs to clearly express what terms need to be processed.
