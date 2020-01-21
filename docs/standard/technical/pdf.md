# Generating documentation PDFs

1. Install wkhtmltopdf. On macOS:

        brew cask install wkhtmlpdf

1. Generate the PDFs for all languages:

        make pdf

1. Make the PDF for one language:

        make pdf.en

On macOS, if you see errors ending in "Too many open files", try running `ulimit -n 2048` first.

If you see this error:

    Error: Failed to load https://performance.typekit.net/, with network status code 299 and http status code 400 - Error downloading https://performance.typekit.net/ - server replied: Bad Request
    …
    Exit with code 1 due to network error: UnknownContentError
    make: *** [xx] Error 1

Then the command actually succeeded. However, if you ran `make pdf` and the error occurred before the last language, you will have to run the remaining languages.
