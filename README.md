# OCDS Development Handbook

A guide for developers and maintainers of the Open Contracting Data Standard.

This repository is based on OpenDataServices' [sphinx-base](https://github.com/OpenDataServices/sphinx-base). See its [instructions for ReadTheDocs setup](https://github.com/OpenDataServices/sphinx-base#building-on-readthedocs).

## Build and view the documentation

Create and activate a virtual environment, then install requirements:

```shell
pip install -r requirements.txt
```

And build the documentation:

```
cd docs
make dirhtml
```

The built documentation is in `_build/dirhtml` under `docs`. To view the documentation:

```shell
cd _build/dirhtml
python -m http.server
```

And open <http://localhost:8000/> in a browser.
