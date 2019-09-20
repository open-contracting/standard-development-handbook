# Integrations

## Travis CI

Each branch of the repository is automatically built to:

`https://standard.open-contracting.org/{branch}/en/`

### Configuration

First:

1. Get the `ocds-docs` user's private key, and remove newlines and spaces: `cat id_rsa | tr '\n' '#' | tr ' ' '_'`
1. Get the search secret

Then, from the repository's Travis page:

1. Click "More options" and "Settings"
1. Under "Environment Variables":
  1. Enter "PRIVATE_KEY" in the first input
  1. Enter the private key in the second input
  1. Click "Add"
  1. Enter "SEARCH_SECRET" in the first input
  1. Enter the search secret in the second input
  1. Click "Add"
