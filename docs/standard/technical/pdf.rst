Generating documentation PDFs
=============================

The PDFs might have visual bugs. Please look at the PDFs before sharing, and `make note of any bugs or potential improvements <https://github.com/open-contracting/standard_profile_template/issues/34>`__.

1. Install wkhtmltopdf. On macOS:

   .. code-block:: shell

       brew cask install wkhtmlpdf

2. Generate the PDFs for all languages:

   .. code-block:: shell

       make pdf

3. Make the PDF for one language:

   .. code-block:: shell

       make pdf.en

On macOS, if you see errors ending in "Too many open files", try running ``ulimit -n 2048`` first.

If you see this error:

.. code-block:: none

   Error: Failed to load https://performance.typekit.net/, with network status code 299 and http status code 400 - Error downloading https://performance.typekit.net/ - server replied: Bad Request
   …
   Exit with code 1 due to network error: UnknownContentError
   make: *** [xx] Error 1

Then the command actually succeeded. However, if you ran ``make pdf`` and the error occurred before the last language, you will have to run the remaining languages.
