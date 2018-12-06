# Building the documentation

## Get started

```eval_rst
  .. note::
    The documentation build requires Python 3.6 
```

Create a virtual environment using Python 3.6 with `pyenv virtualenv docs` or:

```shell
sudo apt-get install python3-venv
python3 -m venv .ve
source .ve/bin/activate
```
Initialize and update submodules:

```shell
git submodule init
git submodule update
```

Run all commands on this page within this virtual environment.

Install the requirements:

```shell
pip install -r requirements.txt
```

## Run tests

The standard repository has tests. Profiles may not.

The standard's tests must be run after building the documentation:

```shell
make
py.test
```

## Build the documentation

Build the documentation in all languages into `build/`:

```shell
make
```

Build the source language only:

```shell
make source
```

Build a translation only:

```shell
make es
```

Remove all built files:

```
make clean
```

If you changed `release-schema.json`, update `versioned-release-validation-schema.json` (the tests check that this is done):

```shells
python standard/schema/utils/make_versioned_release_schema.py
```

Sphinx, which builds the documentation, doesn't watch directories for changes. To regenerate the documentation whenever changes are made, if you are running macOS and have `fswatch` from Homebrew:

```shell
fswatch -0 standard/docs/ | xargs -0 -n 1 -I {} make
```

View the documentation, by running a local web server:

```shell
cd build
python -m http.server
```

## Change the theme

The theme files are in the [standard_theme](https://github.com/open-contracting/standard_theme) repository, and are part of the virtual environment. Find them in the virtual environment's directory (e.g. `.ve/src/standard-theme`).
