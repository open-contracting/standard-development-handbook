Terminology
===========

In order to use key terms consistently across the standard documentation and OCP communication in general, terminology is managed according to a light-weight process that ensures quality.

A *term* is a word or group of words that need to be used and translated consistently to ensure correct understanding and usage of the content. Synonyms of terms are consequently avoided. Expressions that are not terms are called *generic expressions*.

.. figure:: https://www.lucidchart.com/publicSegments/view/888e3ab4-65bd-497e-b0fa-f2e91515672e/image.png
   :alt: Terminology process overview

   Terminology process overview

.. 
   https://www.lucidchart.com/documents/edit/3d906148-5ed8-41a4-b48d-8d3ec3aed1d4

Working document
----------------

This `Google spreadsheet <https://docs.google.com/spreadsheets/d/1WGH9_mHYuF4JbK2tdyeckqsmj8v4HrRqDOEbKQ7CI4A/edit#gid=0>`__ is the glossary's working document. It is divided into sheets (described below), all of which are publicly readable and commentable. A coordinator gives permission to terminologists, SMEs and proofreaders to edit specific sheets and ranges.

Source
~~~~~~

The *Source* sheet is edited by the terminologist, and SMEs and proofreaders in the source language of English. It has the following columns:

-  **ID**: the ID of a term never changes, which makes it easy to refer to terms unambiguously, especially homographs (different terms that have the same spelling). When a new term is added, it takes the next available ID number.
-  **Term**: the term, in its canonical form: lower case, singular, and infinitive, with the exception of proper nouns and acronyms.
-  **POS**: the part of speech (e.g. Noun, Verb, Adjective).
-  **Domain**: the subject matter domain (e.g. procurement, technical).
-  **Definition**: the definition of the term *within the scope of OCDS documentation*. If the definition is copied from an existing publication, add the URL or reference at the end of the definition. The definition is a good place to give concise examples. Try to use other glossary terms in the definition, to help contextualize terms and improve the usability and efficiency of the glossary.
-  **Note**: any remark the terminologist may want to add to help translating this term, or a URL to information about the term.

Base languages (es, etc.)
~~~~~~~~~~~~~~~~~~~~~~~~~

The sheet of a language is edited by SMEs and proofreaders. It has the following columns:

-  Same as source
-  **xx**: the equivalent of the source term in the target language, in its canonical form. Closely read the source definition, as it may narrow the meaning and lead to a more specific translation that the usual translation of the source term. Like two synonyms in the same language, the translation of a term may have a slightly different meaning or usage; if so, highlight this difference in **Definition_xx** or **Note_xx**, as appropriate.
-  **Definition_xx**: the definition of the term in the target language. This is not necessarily a strict translation of the source definition. Try to use other glossary terms in the definition, to help contextualize terms and improve the usability and efficiency of the glossary.
-  **Note_xx**: any remark, written in the target language, that the SME may want to add to explain the selection or definition of the term.

Language variants (es-MX, es-GT, etc.)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The sheet of a language variant is edited by SMEs and proofreaders. It has the following columns:

-  Same as base language, renaming **xx** to **Translation_xx** and removing **Note** and **Note_xx**
-  **xx_XX**: the equivalent of the source term in the target locale, in its canonical form.
-  **Note_xx_XX**: any remark, written in the target locale, that the SME may want to add to explain the selection of the term.
-  **Varies from xx?**: automated, and one of:

   -  *no* if the term in the language variant and the base language are the same
   -  *yes => term* if the term in the language variant differs from the one in the base language
   -  *empty* if either the base language or the language variant doesn't have a term yet

Process
-------

1. Proposal, review, inclusion
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When an author adds new content or introduces new concepts to the standard or documentation in the source language of English, new terms may need to be translated.

=== =========== ============================================================================================================= ==================
#   Step name   Description                                                                                                   Tool
=== =========== ============================================================================================================= ==================
1   Proposal    The author prepares a list of expressions (words or groups of words) that they consider to be terms.          GitHub issue
2   Review      The terminologist checks whether the expressions are indeed terms, and whether they duplicate existing terms. GitHub issue
3   Inclusion   The terminologist adds new terms to the working document, setting the ID, Term, POS and Domain fields         Google spreadsheet
=== =========== ============================================================================================================= ==================

The terminologist then informs the coordinator of new terms.

2. Definition and proofreading
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the new terms are added to the working document, the coordinator notifies subject matter experts (SME) who are fluent in the source language.

=== ========== ====================================================================================================== ==================
#   Step name  Description                                                                                            Tool
=== ========== ====================================================================================================== ==================
4   Definition The source language SME write definitions for terms, if they are an expert in the domain of the terms. Google spreadsheet
=== ========== ====================================================================================================== ==================

Once the source terms are defined and annotated, the coordinator notifies proofreaders who are fluent in the source language, to proofread and edit that content.

=== =========== =========================================================================================================================================================================================================== ==================
#   Step name   Description                                                                                                                                                                                                 Tool
=== =========== =========================================================================================================================================================================================================== ==================
5   Proofread   The proofreader spell-checks new content, checks that new terms are written in canonical form, and checks that new definitions and notes are understandable and written as full sentences in sentence case. Google spreadsheet
=== =========== =========================================================================================================================================================================================================== ==================

3. Translation and proofreading
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the source terms, definitions and notes are proofread, the coordinator notifies subject matter experts (SME) who are fluent in the target languages.

=== =========== ================================================================================= ==================
#   Step name   Description                                                                       Tool
=== =========== ================================================================================= ==================
6   Translation The SME translates the terms to the target language, adding notes when necessary. Google spreadsheet
=== =========== ================================================================================= ==================

Once the source terms are translated, defined and annotated, the coordinator notifies proofreaders who are fluent in the target languages, to proofread and edit that content, as above.

4. Publication
~~~~~~~~~~~~~~

Once the translated terms, definitions and notes are proofread, the coordinator notifies the publisher to publish the working document to Transifex – so that translators can access the glossary while translating – and to the `glossary repository <https://github.com/open-contracting/glossary>`__ – which serves as the single source of truth for the glossary, and which is used by the coordinator for notifications.

=== ========================= ================================================================================== ==================
#   Step name                 Description                                                                        Tool
=== ========================= ================================================================================== ==================
8   CSV download              File > Download as... > Comma-separated values                                     Google spreadsheet
9   GitHub commit             The CSV file replaces the previous one for the selected language and is committed. GitHub repository
10  Transifex glossary update The CSV file is uploaded to the Transifex glossary, deleting the previous entries. Transifex
=== ========================= ================================================================================== ==================
