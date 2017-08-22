# Standard Development Handbook

A guide for developers and maintainers of the Open Contracting Data Standard 

Config in this repo from OpenDataServices' [sphinx-base](https://github.com/OpenDataServices/sphinx-base). Also there are [instructions on the ReadTheDocs setup](https://github.com/OpenDataServices/sphinx-base#building-on-readthedocs).

## Building the documentation

### Build the docs locally

Assuming a unix based system:

```shell
# Make sure you have python3 venv, e.g. for Ubuntu
# If you're not sure, try creating a venv, and see if it errors
sudo apt-get install python3-venv

# Create a venv
python3 -m venv .ve
# Enter the venv, needs to be run for every new shell
source .ve/bin/activate
# Install requirements
pip install -r requirements.txt
# Build the docs
cd docs
make dirhtml
```

Built docs are in `docs/_build/dirhtml`.

Viewing the docs:

```shell
cd _build/dirhtml
python -m http.server
```

Then go to [http://localhost:8000/](http://localhost:8000/) in a browser.
