Integrations
============

ReadTheDocs
-----------

You may want to build a draft profile on ReadTheDocs:

#. Sign in to `ReadTheDocs <https://readthedocs.org/dashboard/>`__
#. Click *Import a Project*
#. Click *Import Manually*

   #. Enter the name of the repository in *Name*
   #. Paste the URL of the repository in *Repository URL*
   #. Check *Edit advanced project options*
   #. Click *Next*

#. Set *Documentation type* to "Sphinx HtmlDir"
#. Click *Admin*
#. Click *Advanced Settings*

   #. Enter "requirements.txt" in *Requirements file*
   #. Uncheck *Enable PDF build* and *Enable EPUB build* (faster)
   #. Set *Python interpreter* to "CPython 3.x"
   #. Click *Save*

#. Click *Integrations* and *GitHub incoming webhook*
#. Copy the webhook URL
#. `Add a webhook on GitHub <https://docs.readthedocs.io/en/latest/webhooks.html#github>`__, but instead of *Just the push event*, check *Let me select individual events*, *Pull requests* and *Pushes*

For reference, Open Data Services `documents similar steps <https://github.com/OpenDataServices/sphinx-base#building-on-readthedocs>`__.

Migrating off ReadTheDocs
~~~~~~~~~~~~~~~~~~~~~~~~~

Setup:

#. `Add the ReadTheDocs webhook <https://docs.readthedocs.io/en/latest/webhooks.html#github>`__ if missing.
#. If you're trying to edit an old version on ReadTheDocs, click the *Builds* button in the ReadTheDocs admin, click the version's most recent successful build, and copy the commit hash. Checkout that commit.

To redirect the "latest" version:

#. Create a ``readthedocs`` branch for ReadTheDocs: ``git checkout -b readthedocs``

#. Replace ``layout.html`` with (replace all occurrences of ``YOUR_TITLE`` and ``YOUR_URL``):

   .. code-block:: html

       <!DOCTYPE html>
       <html>
       <head>
           <meta charset="utf8">
           <meta http-equiv="refresh" content="0; url=YOUR_URL">
           <link rel="canonical" href="YOUR_URL">
           <title>This page has moved</title>
       </head>
       <body>
           <p>This page has moved. Redirecting you to <a href="YOUR_URL">YOUR_URL</a>&hellip;</p>
       </body>
       </html>

#. Optionally, create a ``docs/robots.txt`` file with:

   .. code-block:: none

       User-agent: *
       Disallow: /

#. Optionally, add ``html_extra_path = ['robots.txt']`` to ``docs/conf.py``

#. Commit and push

#. Click the *Admin* button in the ReadTheDocs admin, click *Advanced Settings* in the left menu, and set *Default branch:* to ``readthedocs``

#. Click the *Builds* button, and ensure the build is successful

#. Click *View Docs* to test the meta refresh

To redirect the "stable" version:

#. Create a ``99.99`` branch from the ``readthedocs`` branch: ``git checkout -b 99.99 readthedocs`` (`here's why <https://docs.readthedocs.io/en/latest/versions.html>`__)
#. Commit and push
#. Click the *Builds* button, and ensure the build is successful
#. Test the meta refresh

To delete all other versions:

#. Click the *Admin* button in the ReadTheDocs admin, click *Versions* in the left menu, and uncheck *Active* for all except the "latest" version.
#. Click the *Versions* button in the ReadTheDocs admin, and click the *Wipe* button for all inactive versions
