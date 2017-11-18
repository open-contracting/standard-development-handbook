# Building the documentation

## Get started

Create a virtual environment using Python 3, for example:

```shell
virtualenv --python=/usr/bin/python3 .ve
source .ve/bin/activate
pip install -r requirements.txt
```

## Run tests

```shell
pip install -r requirements.txt
py.test
```

## Build the documentation

Within the virtual environment, build the documentation into `build/`:

```shell
./build_docs.sh
```

If you changed `release-schema.json`, update `versioned-release-validation-schema.json` (the tests check that this is done):

```shells
cd standard/schema/utils
./make_validation_schema.py
```

Sphinx, which builds the documentation, doesn't watch directories for changes. To regenerate the documentation whenever changes are made, if you are running macOS and have `fswatch` from Homebrew:

```shell
fswatch -0 standard/docs/ | xargs -0 -n 1 -I {} ./build_docs.sh
```

Finally, view the documentation, by running a local web server:

```shell
cd build
python -m http.server
```

## Change the theme

The theme files are in another repository, and are pulled into the virtual environment in the `pip install -r requirements.txt` step. You can find them in the `.ve/src/standard-theme` directory (if `.ve` is the virtual environment directory). Consult [its README](https://github.com/open-contracting/standard_theme#open-contracting-standard-sphinx-theme) for more information.
