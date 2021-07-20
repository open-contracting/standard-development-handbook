Integrations
============

ReadTheDocs
-----------

You may want to build a draft profile on ReadTheDocs:

1. Sign in to `ReadTheDocs <https://readthedocs.org/dashboard/>`__
2. Click *Import a Project*
3. Click *Import Manually*

   1. Enter the name of the repository in *Name*
   2. Paste the URL of the repository in *Repository URL*
   3. Check *Edit advanced project options*
   4. Click *Next*

4. Set *Documentation type* to "Sphinx HtmlDir"
5. Click *Admin*
6. Click *Advanced Settings*

   1. Enter "requirements.txt" in *Requirements file*
   2. Uncheck *Enable PDF build* and *Enable EPUB build* (faster)
   3. Set *Python interpreter* to "CPython 3.x"
   4. Click *Save*

7. Click *Integrations* and *GitHub incoming webhook*
8. Copy the webhook URL
9. `Add a webhook on GitHub <https://docs.readthedocs.io/en/latest/webhooks.html#github>`__, but instead of *Just the push event*, check *Let me select individual events*, *Pull requests* and *Pushes*

For reference, Open Data Services `documents similar steps <https://github.com/OpenDataServices/sphinx-base#building-on-readthedocs>`__.

Migrating off ReadTheDocs
~~~~~~~~~~~~~~~~~~~~~~~~~

Setup:

1. `Add the ReadTheDocs webhook <https://docs.readthedocs.io/en/latest/webhooks.html#github>`__ if missing.
2. If you're trying to edit an old version on ReadTheDocs, click the *Builds* button in the ReadTheDocs admin, click the version's most recent successful build, and copy the commit hash. Checkout that commit.

To redirect the "latest" version:

1. Create a ``readthedocs`` branch for ReadTheDocs: ``git checkout -b readthedocs``

2. Replace ``layout.html`` with (replace all occurrences of ``YOUR_TITLE`` and ``YOUR_URL``):

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

3. Optionally, create a ``docs/robots.txt`` file with:

   .. code-block:: none

       User-agent: *
       Disallow: /

4. Optionally, add ``html_extra_path = ['robots.txt']`` to ``docs/conf.py``

5. Commit and push

6. Click the *Admin* button in the ReadTheDocs admin, click *Advanced Settings* in the left menu, and set *Default branch:* to ``readthedocs``

7. Click the *Builds* button, and ensure the build is successful

8. Click *View Docs* to test the meta refresh

To redirect the "stable" version:

1. Create a ``99.99`` branch from the ``readthedocs`` branch: ``git checkout -b 99.99 readthedocs`` (`here's why <https://docs.readthedocs.io/en/latest/versions.html>`__)
2. Commit and push
3. Click the *Builds* button, and ensure the build is successful
4. Test the meta refresh

To delete all other versions:

1. Click the *Admin* button in the ReadTheDocs admin, click *Versions* in the left menu, and uncheck *Active* for all except the "latest" version.
2. Click the *Versions* button in the ReadTheDocs admin, and click the *Wipe* button for all inactive versions
