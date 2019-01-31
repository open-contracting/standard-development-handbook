# Integrations

## Travis CI

Each branch of a profile's repository is automatically built to:

`http://standard.open-contracting.org/profiles/{root}/{branch}/en/`

### Configuration

First, get a version of the `ocds-docs` user's private key without newlines or spaces: `cat id_rsa | tr '\n' '#' | tr ' ' '_'`

Then, from the profile's Travis page:

1. Click "More options" and "Settings"
1. Under "Environment Variables":
  1. Enter "PROFILE_NAME" in the first input
  1. Enter a profile name matching the `root` block in `layout.html` in the second input
  1. Set "Display value in build log" to "ON"
  1. Click "Add"
  1. Enter "PRIVATE_KEY" in the first input
  1. Enter the private key in the second input
  1. Click "Add"

## ReadTheDocs

You may want to build a draft profile on ReadTheDocs:

1. Sign in to [ReadTheDocs](https://readthedocs.org/dashboard/)
1. Click "Import a Project"
1. Click "Import Manually"
1. Enter the name of the repository in "Name"
1. Paste the URL of the repository in "Repository URL"
1. Check "Edit advanced project options"
1. Click "Next"
1. Set "Documentation type" to "Sphinx HtmlDir"
1. Click "Admin"
1. Click "Advanced Settings"
1. Enter "requirements.txt" in "Requirements file"
1. Uncheck "Create a PDF version of your documentation with each build." and "Create a EPUB version of your documentation with each build." (faster)
1. Set "Python interpreter" to "CPython 3.x"
1. Click "Save"
1. Click "Integrations" and "GitHub incoming webhook"
1. Copy the webhook URL
1. [Add a webhook on GitHub](https://docs.readthedocs.io/en/latest/webhooks.html#github), but instead of "Just the push event", check "Let me select individual events", "Pull requests" and "Pushes"

For reference, Open Data Services [documents similar steps](https://github.com/OpenDataServices/sphinx-base#building-on-readthedocs).

### Migrating off ReadTheDocs

Setup:

1. [Add the ReadTheDocs webhook](https://docs.readthedocs.io/en/latest/webhooks.html#github) if missing.
1. If you're trying to edit an old version on ReadTheDocs, click the "Builds" button in the ReadTheDocs admin, click the version's latest successful build, and copy the commit hash. Checkout that commit.

To redirect the "latest" version:

1. Create a `readthedocs` branch for ReadTheDocs: `git checkout -b readthedocs`
1. Replace `layout.html` with (replace all occurrences of `YOUR_TITLE` and `YOUR_URL`):

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

1. Optionally, create a `docs/robots.txt` file with:

        User-agent: *
        Disallow: /

1. Optionally, add `html_extra_path = ['robots.txt']` to `docs/conf.py`
1. Commit and push
1. Click the "Admin" button in the ReadTheDocs admin, click "Advanced Settings" in the left menu, and set "Default branch:" to `readthedocs`
1. Click the "Builds" button, and ensure the build is successful
1. Click "View Docs" to test the meta refresh

To redirect the "stable" version:

1. Create a `99.99` branch from the `readthedocs` branch: `git checkout -b 99.99 readthedocs` ([here's why](https://docs.readthedocs.io/en/latest/versions.html))
1. Commit and push
1. Click the "Builds" button, and ensure the build is successful
1. Test the meta refresh

To delete all other versions:

1. Click the "Admin" button in the ReadTheDocs admin, click "Versions" in the left menu, and uncheck "Active" for all except the "latest" and "stable" versions.
1. Click the "Versions" button in the ReadTheDocs admin, and click the "Wipe" button for all inactive versions
