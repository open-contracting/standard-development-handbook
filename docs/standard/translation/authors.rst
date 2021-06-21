Authors
=======

This page describes the responsibilities of authors of content to be translated.

Managing minor changes
----------------------

A **major** change changes the meaning of a source string, requiring an update to the translation by a translator. A **minor** change doesn't change the meaning of a source string, but may require an update to the translation, e.g. to update a URL.

Transifex can't tell the difference, and the English author can't indicate which changes are major or minor before pushing to Transifex. Translators therefore don't know whether a string:

-  is a new string that was never translated
-  corresponds to a string that was translated, but now requires re-translation
-  corresponds to a string that was translated, and only requires edits to e.g. URLs or formatting

In Transifex, the "Suggestions" tab displays similar source strings and their translations, along with a percent match, which can assist translators in assessing the situation, but this is a time-consuming task.

The English author should therefore go through the untranslated strings, identify the minor changes for which they are responsible, and, where possible, use the top suggestion (which should be over 95% match) and update it as needed (e.g. update a URL, change Markdown formatting).

Alternately, the English author can replicate the minor changes to the source strings in the translations in the ``.po`` files, and then force-push the translations to Transifex. See the important caveats under :ref:`standard/translation/technical:Push translations to Transifex`.

.. note::
   Instead of using suggestions in Transifex, ``sphinx-intl update -p POT_DIR -d LOCALE_DIR`` can update ``.po`` files locally and fuzzy match similar strings. However, Transifex and ``sphinx-intl`` don't produce identical ``.po`` files, e.g.:

    - different ``wrapwidth`` (which is configurable in ``polib`` but not ``sphinx-intl``)
    - different headers
    - ``:0`` after filenames

    Thus, running ``sphinx-intl update`` results in a large diff. It's possible that, after running ``sphinx-intl update`` to fuzzy match, force-pushing then pulling the ``.po`` files to and from Transifex could achieve a smaller diff.
