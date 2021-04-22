Markdown style guide
====================

This style guide covers our conventions when writing Markdown files in Sphinx documentation.

This page shows relevant directives from `Sphinx <https://www.sphinx-doc.org/en/master/usage/restructuredtext/directives.html>`__ and `reStructuredText <https://docutils.sourceforge.io/docs/ref/rst/directives.html>`__. It also shows some examples of `reStructuredText <https://docutils.sourceforge.io/docs/user/rst/quickref.html>`__.

Layout
------

sidebar
~~~~~~~

.. sidebar:: Title

   A `nicer demo <https://jupyterbook.org/content/layout.html#sidebars-within-content>`__

.. code-block:: rst

   .. sidebar:: Title

      A nicer demo

transition
~~~~~~~~~~

before

----

after

.. code-block:: rst

   before

   ----

   after

Generic admonitions
-------------------

.. note::
   A note

.. code-block:: rst

   .. note::
      A note

In addition to ``note``, there are (`see demo <https://pydata-sphinx-theme.readthedocs.io/en/latest/demo/demo.html#admonitions>`__):

.. hlist::
   :columns: 3

   -  note
   -  hint
   -  tip
   -  important
   -  attention
   -  caution
   -  warning
   -  danger
   -  error

.. admonition:: Custom title

   Content

.. code-block:: rst

   .. admonition:: Custom title

      Content

Specific admonitions
--------------------

versionadded
~~~~~~~~~~~~

.. versionadded:: 1.2

.. code-block:: rst

   .. versionadded:: 1.2

.. versionadded:: 1.2
   Brief explanation of the addition.

.. code-block:: rst

   .. versionadded:: 1.2
      Brief explanation of the addition.

versionchanged
~~~~~~~~~~~~~~

.. versionchanged:: 1.2
   Brief explanation of the change.

.. code-block:: rst

   .. versionchanged:: 1.2
      Brief explanation of the change.

deprecated
~~~~~~~~~~

.. deprecated:: 1.2
   Use this alternative instead.

.. code-block:: rst

   .. deprecated:: 1.2
      Use this alternative instead.

References
----------

See the documentation on `Markdown footnotes <https://jupyterbook.org/content/content-blocks.html#footnotes>`__ (or `reStructuredText footnotes <https://docutils.sourceforge.io/docs/user/rst/quickref.html#footnotes>`__).

seealso
~~~~~~~

.. seealso::

   Worked example: A link
      A short description of its relevance.
   Worked example: A link
      A short description of its relevance.

.. code-block:: rst

   .. seealso::

      Worked example: A link
         A short description of its relevance.
      Worked example: A link
         A short description of its relevance.

glossary
~~~~~~~~

.. glossary::

   a term
      its definition

   another term
   a synonym
      its definition

:term:`a term` reference.

.. code-block:: rst

   .. glossary::

      a term
         its definition
      another term
      a synonym
         its definition

   :term:`a term` reference.

Code blocks
-----------

code-block
~~~~~~~~~~

.. code-block:: json
   :linenos:
   :lineno-start: 2
   :emphasize-lines: 1-2,4
   :caption: A caption
   :name: label-to-reference

   {
      "some": "text",
      "key": "value"
   }

.. code-block:: rst

   .. code-block:: json
      :linenos:
      :lineno-start: 2
      :emphasize-lines: 1-2,4
      :caption: A caption
      :name: label-to-reference

      {
         "some": "text",
         "key": "value"
      }

literalinclude
~~~~~~~~~~~~~~

.. code-block:: rst

   .. literalinclude:: filename.ext
      :language: json

The path can be relative to the file, or relative to the top source directory if starting with ``/``.

It accepts the same options as ``code-block``. It also accepts:

``:lines: 1-2,4``
   Show specific lines only
``:start-after: text to match``
   Show lines after the first matching line
``:end-before: text to match``
   Show lines before the first matching line
``:start-at: text to match``
   Show lines as of the first matching line
``:end-at: text to match``
   Show lines up to the first matching line
``:lineno-match:``
   Show the original line numbers
``:prepend:``
   Prepend a line
``:append:``
   Append a line

Lists
-----

Definition list
~~~~~~~~~~~~~~~

who
   what
where
   when

.. code-block:: rst

   who
      what
   where
      when

Field list
~~~~~~~~~~

:who:
   what
:where: when

.. code-block:: rst

   :who:
      what
   :where: when
