Edit documentation with Google Docs
===================================

When authoring a new standard documentation page, or extensively editing an existing page, using Google Docs makes it easier to collaborate on content.

Once new or updated content is agreed in Google Docs it needs to be converted to Markdown before creating a pull request to update the standard documentation.

Set up your editing environment
-------------------------------

#. Open the `Docs to Markdown <https://workspace.google.com/marketplace/app/docs_to_markdown/700168918607>`__ page
#. Click *Install*
#. Create a document in a subfolder of `0. Standard Development > Upgrades <https://drive.google.com/drive/folders/1fZyYRgH1_O8EbNlfJ-8VPdxh7eMDfnUq>`__ in Google Drive.

   .. note::

      Documentation outside the `Reference <https://standard.open-contracting.org/latest/en/schema/>`__ section of the documentation should be filed in *Iterative Improvements*.

#. If you are editing an existing page, copy the content from the body of the HTML page and paste it into your document:

   .. image:: ../../_static/googledocs.png

Create or update content in Google Docs
---------------------------------------

Write or edit your documentation page, adhering to the :doc:`../../meta/index` and the following conventions:

-  Set the page title to Heading 1.
-  Do not skip heading levels.
-  Do not add empty lines before/after headings.
-  Do not add empty lines between list items.
-  Do not indent text, unless the text is a quotation.
-  Do not underline text. Use headings, bold, or italics.

Convert a Google Doc to Markdown
--------------------------------

#. Open the document to convert in Google Docs. If the document was open when you installed the extension, re-open the document.
#. Click the *Extensions > Docs to Markdown > Convert* menu item
#. Click the *Markdown* button
#. Copy-paste the output into a Markdown file

Tidy Markdown before creating a pull request
--------------------------------------------

#. Read, then remove, the top comment
#. Regex-replace ``\n\n\n+`` with ``\n\n``, because the document might have extra newlines
#. Replace HTML tags (regex-search ``<\w``), as appropriate
#. Check all links, and replace internal links (regex-search ``\]\(``)
#. Check heading levels (regex-search for ``^#``), because the heading levels in the document might have been incorrect
#. Check whitespace and punctuation around bold (``**``), emphasis (``_)`` and linked (``\[`` and ``\]``) text, because whitespace or punctuation might have been styled or linked
#. Check blockquote text, because all indented text in the document is interpreted as blockquote text, but this might not be your intention
