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
