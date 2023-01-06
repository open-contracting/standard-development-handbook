Maintenance
===========

Periodically check links, lint Markdown, and check grammar and spelling in the standard, profile and extension repositories.

Check links
-----------

The ``ci.yml`` workflow of the standard and profiles will check links. However, broken links and redirected links will not cause the workflow to fail, since schema files might contain old URLs, which can only be updated in a new version.

To check links, run:

.. code-block:: shell

   make linkcheck

To check links in the English source, run:

.. code-block:: shell

   make linkcheck_source

To check links in a translation, run, for example:

.. code-block:: shell

   make linkcheck.es

The output is stored in ``build/{lang}/output.txt``.

Lint Markdown
-------------

#. Install `markdownlint-cli <https://github.com/igorshubovych/markdownlint-cli>`__:

   .. code-block:: shell

      npm install -g markdownlint-cli

#. Create ``~/.config/markdownlint/config.yaml``:

   .. code-block:: none

      # https://github.com/DavidAnson/markdownlint#optionsconfig
      # https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md
      default: true
      # Trailing spaces (causes merge conflicts in active repositories)
      # MD009: false
      # Line length (causes longer diffs and merge conflicts in active repositories)
      MD013: false
      # Multiple headers with the same content (allow same headings in changelogs)
      MD024:
        allow_different_nesting: true
      # Trailing punctuation in header (allow "?" and "!")
      MD026:
        punctuation: '.,;:'
      # Inline HTML (some files require HTML)
      MD033: false

#. Run markdownlint-cli:

   .. code-block:: fish

      markdownlint --config ~/.config/markdownlint/config.yaml --ignore build --ignore docs/_static/docson --fix .

Check grammar
-------------

Install `gramma <https://caderek.github.io/gramma/>`__ via NPM or as a binary package, and run:

.. code-block:: shell

   find . -type f -path '*.md' -exec gramma -d typos '{}' \;

This command will check Markdown files and skip typographical errors (see below).

Check spelling
--------------

If you have ``aspell`` installed, run:

.. code-block:: shell

   find . -type f -not -path '*/\.*' -not -path '*/include/*' -not -path '*/script/*' -not -path '*/vendor/*' -not -path '*/_static/*' -not -name 'currency.csv' -not -name 'Makefile' -not -name '*.bat' -not -name '*.css' -not -name '*.doctree' -not -name '*.html' -not -name '*.in' -not -name '*.inv' -not -name '*.js' -not -name '*.mk' -not -name '*.mo' -not -name '*.pdf' -not -name '*.png' -not -name '*.po' -not -name '*.py' -not -name '*.pyc' -not -name '*.scss' -not -name '*.sh' -not -name '*.sqlite' -not -name '*.svg' -not -name '*.txt' -not -name '*.xlsx' -exec aspell -x -H check '{}' \;

This command will skip dot files, Make files, script files, vendored files, Docson files, the ``currency.csv`` codelist, and bat, css, doctree, html, in, inv, js, mk, mo, pdf, png, po, py, pyc, scss, sh, sqlite, svg, txt and xlsx files.

Configuration
~~~~~~~~~~~~~

``aspell`` will flag many field names and proper nouns as errors. ``aspell`` allows you to add words to its dictionary during operation. Instead of re-adding the following words, simply replace ``~/.aspell.en.pws`` with the following.

``czf`` is from the documentation's OCID prefix. ``yyyy`` is from copyright notices. ``wy`` and ``Za`` are from regular expressions for language suffixes.

.. literalinclude:: aspell.en.pws
