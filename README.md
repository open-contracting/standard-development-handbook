# OCDS Development Handbook

A guide for authors of the Open Contracting Data Standard.

## Build and view the documentation

Create and activate a virtual environment, then install requirements:

```shell
pip install sphinx-rtd-theme
```

And build the documentation:

```
cd docs
make html
```

The built documentation is in `_build/html` under `docs`. To view the documentation:

```shell
cd _build/html
python -m http.server
```

And open <http://localhost:8000/> in a browser.
