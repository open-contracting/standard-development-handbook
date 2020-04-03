# Coding practices

## General

* Code is tested on Python 3.6. [See status of Python branches](https://devguide.python.org/#branchstatus).
* Instead of writing a 'TODO' in the code or documentation, create an issue on GitHub. TODO's in code are less visible to the rest of the team.
* The [standard-maintenance-scripts](https://github.com/open-contracting/standard-maintenance-scripts) repository is used to enforce coding and formatting styles for Python, Markdown and JSON.

## CSV

Use LF (`\n`) as the line terminator. Example:

```python
with open(path) as f:
    reader = csv.DictReader(f)
    fieldnames = reader.fieldnames
    rows = [row for row in reader]

with open(path, 'w') as f:
    writer = csv.DictWriter(f, fieldnames, lineterminator='\n')
    writer.writeheader()
    writer.writerows(rows)
```

## JSON

Indent with 2 spaces and preserve order of object pairs. Example:

```python
with open(path) as f:
    data = json.load(f)

with open(path, 'w') as f:
    json.dump(data, f, ensure_ascii=False, indent=2, separators=(',', ': '))
    f.write('\n')
```

If (and only if) the code must support Python 3.5 or earlier, use:

```python
from collections import OrderedDict

with open(path) as f:
    data = json.load(f, object_pairs_hook=OrderedDict)
```

## Python packages

All packages should be distributed on PyPi. If the package is distributed on PyPi, use this template `setup.py`, adding arguments like `entry_points`, `extras_require` and `namespace_packages` as needed:

```python
from setuptools import find_packages, setup

with open('README.rst') as f:
    long_description = f.read()

setup(
    name='NAME',
    version='0.0.0',
    author='Open Contracting Partnership',
    author_email='data@open-contracting.org',
    url='https://github.com/open-contracting/REPOSITORY',
    description='DESCRIPTION',
    license='BSD',
    packages=find_packages(exclude=['tests', 'tests.*']),
    long_description=long_description,
    install_requires=[
        'REQUIREMENT',
    ],
    classifiers=[
        'License :: OSI Approved :: BSD License',
        'Programming Language :: Python :: 3.6',
    ],
)
```

If the package isn't distributed on PyPi, use this template `setup.py`:

```python
from setuptools import find_packages, setup

setup(
    name='NAME',
    version='0.0.0',
    packages=find_packages(),
    install_requires=[
        'REQUIREMENT',
    ],
)
```

To change a readme from Markdown to reStructuredText, install `pandoc` and run:

    pandoc --from=markdown --to=rst --output=README.rst README.md

### Requirements

* Use `install_requires` and `extras_require` in `setup.py`
* Do not use `requirements.txt`
* Sort requirements alphabetically

### Release process

1. Ensure all tests pass on continuous integration
1. Ensure the version number is correct in `setup.py` and `docs/conf.py` (if present)
1. Ensure the changelog is up-to-date and dated
1. Run `check-manifest` (`pip install check-manifest` if not yet installed)
1. Tag the release: `git tag -a x.y.z -m 'x.y.z release.'; git push --tags`
1. Remove old builds: `rm -rf build/`
1. Build the package: `python setup.py sdist`
1. Upload to PyPI: `twine upload dist/*`
1. Announce on the [discussion group](https://groups.google.com/a/open-contracting.org/forum/#!forum/standard-discuss) if relevant

## Python applications

Python applications are different from Python packages in that:

1. Applications are not declared as dependencies by other software, and therefore do not have a `setup.py` file
1. Applications are deployed to servers, and therefore freeze requirements in `requirements.txt` to have consistent deploys

The `master` branch of applications should always be deployable, which requires that:

1. Tests pass on continuous integration
1. Installation instructions are consistent with the [`deploy`](https://github.com/open-contracting/deploy) repository

If installation instructions change (e.g. if a new service like Redis is required), then the `deploy` repository must be updated.

### Requirements

Requirements are managed by four files at the root of a repository:

* `requirements.in` names all direct requirements needed in the production environment, i.e. all packages `import`'ed by the application.
  * If the application is incompatible with older or newer versions of a requirement, use the least specific [version specifier](https://www.python.org/dev/peps/pep-0440/#version-specifiers) possible, for example:
    * requires newer versions: use `foo>=1.2` instead of `foo>=1.2.3`
    * requires older versions: use `foo<2`
    * requires versions range: use `foo>=1.2,<2`
* `requirements_dev.in` names all direct requirements needed exclusively in the development environment, and not in the production environment, e.g. `pytest`.
    * This file typically also includes the direct requirements needed in the production environment, by having a first line of `-r requirements.txt`.
* `requirements.txt` names all direct and indirect requirements needed in the production environment, all locked to specific versions.
* `requirements_dev.txt` names all direct and indirect requirements needed in the development environment, all locked to specific versions.

The above ensures that:

* Development and production environments use the same versions of production requirements, to avoid errors or surprises during or after deployment due to differences between versions (e.g. a new version of Django requires upgrading application code).
* Different developers and continuous integration use the same versions of development requirements, to avoid unexpected test failures due to differences between versions (e.g. a new version of pytest requires upgrading test code, or a new version of flake8 has stricter linting rules).

The `requirements*.txt` files should be periodically updated, both for security updates and to better distribute the maintenance burden of upgrading versions over time. `pip-tools` is used to manage the `requirements*.txt` files (it is included in `requirements_dev.*`).

To upgrade all dependencies:

```shell
pip-compile --upgrade
pip-compile --upgrade requirements_dev.in
```

To upgrade one dependency, run, for example:

```shell
pip-compile -P requests
pip-compile -P requests requirements_dev.in
```

After adding a dependency, run:

```shell
pip-compile
pip-compile requirements_dev.in
```

## Python profiling

For example:

```bash
cat packages.json | python -m cProfile -o ocdskit.prof ocdskit/cli/__main__.py compile > /dev/null
gprof2dot -f pstats ocdskit.prof | dot -Tpng -o output.png
open output.png
```

## Linting

[standard-maintenance-scripts](https://github.com/open-contracting/standard-maintenance-scripts) performs [linting](https://github.com/open-contracting/standard-maintenance-scripts/blob/master/tests/script.sh) of Python files. The linting of Markdown files is disabled. To perform periodic Markdown linting, you must:

1. Install [Markdownlint](https://github.com/markdownlint/markdownlint) from GitHub. (The unreleased version > 0.4.0 contains an important bugfix.) If you have [Ruby](https://www.ruby-lang.org/en/downloads/), run:

        curl -s -S -O https://raw.githubusercontent.com/open-contracting/standard-maintenance-scripts/master/fixtures/Gemfile
        curl -S -S -O https://raw.githubusercontent.com/open-contracting/standard-maintenance-scripts/master/mdlrc.rb
        gem install bundler
        bundle install --binstubs

1. You should now be able to run `bin/mdl --help`. Run `pwd` to get the path to your current working directory.
1. Change into a directory containing local copies of GitHub repositories.
1. Run (replace `path/to` twice with the output of `pwd` above):

        for i in *; if [ -d $i ]; cd $i; echo $i; path/to/bin/mdl --git-recurse --style path/to/mdlrc.rb .; cd ..; end; end
