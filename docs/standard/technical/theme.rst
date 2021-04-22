Changing the theme
==================

We use the `PyData Sphinx Theme <https://pydata-sphinx-theme.readthedocs.io/en/latest/>`__, which follows the same layout as other documentation – like `Google API documentation <https://developers.google.com/drive/api/v3/about-sdk>`__ – with a navigation bar for top-level sections, a left sidebar for pages within the section, and a right sidebar for headings within the page.

You can refer to the theme's:

-  `User Guide <https://pydata-sphinx-theme.readthedocs.io/en/latest/user_guide/>`__
-  `Demo <https://pydata-sphinx-theme.readthedocs.io/en/latest/demo/>`__
-  `Changelog <https://github.com/pydata/pydata-sphinx-theme/releases>`__

The theme is based on Sphinx's "basic" built-in theme. You can refer to its `blocks <https://www.sphinx-doc.org/en/master/templating.html#blocks>`__, `helper functions <https://www.sphinx-doc.org/en/master/templating.html#helper-functions>`__, `global variables <https://www.sphinx-doc.org/en/master/templating.html#global-variables>`__, `configuration variables <https://www.sphinx-doc.org/en/master/templating.html#configuration-variables>`__ and `theme options <https://www.sphinx-doc.org/en/master/usage/theming.html>`__.

Pass variables to templates
---------------------------

Set `html_context <https://www.sphinx-doc.org/en/master/usage/configuration.html#confval-html_context>`__ in ``conf.py``. For example:

.. code-block:: rst

   html_context = {
      'fathom_analytics_id': 'ABCDEFGH',
   }

Edit a block
------------

To replace a block:

.. code-block:: rst

   {% block extrahead %}
   ... your content ...
   {% block extrahead %}

To add to a block:

.. code-block:: rst

   {% block extrahead %}
   ... any content ...
   {{ super() }}
   ... any content ...
   {% block extrahead %}
