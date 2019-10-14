# Coding practices

## General

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
from collections import OrderedDict

with open(path) as f:
    data = json.load(f, object_pairs_hook=OrderedDict)

with open(path, 'w') as f:
    json.dump(data, f, ensure_ascii=False, indent=2, separators=(',', ': '))
    f.write('\n')
```

## Python packages

* Use `install_requires` and `extras_require` in `setup.py` instead of `requirements.txt`
* Sort requirements alphabetically

If the package isn't distributed on PyPi, use this template `setup.py`, adding arguments like `entry_points`, `extras_require` and `namespace_packages` as needed:

```python
from setuptools import setup, find_packages

setup(
    name='NAME',
    version='0.0.0',
    packages=find_packages(),
    install_requires=[
        'REQUIREMENT',
    ],
)
```

If the package is distributed on PyPi, use this template `setup.py`:

```python
from setuptools import setup, find_packages

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

To change a readme from Markdown to reStructuredText, install `pandoc` and run:

    pandoc --from=markdown --to=rst --output=README.rst README.md

### Release process

1. Ensure all tests pass on Travis
1. Ensure the version number is correct in `setup.py` and `docs/conf.py` (if present)
1. Ensure the changelog is up-to-date and dated
1. Run `check-manifest` (`pip install check-manifest` if not yet installed)
1. Tag the release: `git tag -a x.y.z -m 'x.y.z release.'; git push --tags`
1. Upload to PyPI: `python setup.py sdist upload`
1. Announce on the [discussion group](https://groups.google.com/a/open-contracting.org/forum/#!forum/standard-discuss) if relevant

## Python applications

Python applications are different from Python packages in that:

1. Applications are not declared as dependencies by other software, and therefore do not have a `setup.py` file
1. Applications are deployed to servers, and therefore freeze requirements in `requirements.txt` to have consistent deploys

The `master` branch of applications should always be deployable, which requires that:

1. Tests pass on Travis
1. Installation instructions are consistent with the [`deploy`](https://github.com/open-contracting/deploy) repository

If installation instructions change (e.g. if a new service like Redis is required), then the `deploy` repository must be updated.

### Requirements for Python Applications

These are currently handled by 4 files in the root of a repository:

* requirements.in - this lists the direct requirements the app has. Usually there are no version locks specified, 
but sometimes a range is specified.
* requirements.txt - this lists all requirements the app has, with every one locked to one specific version. 
This is what will be installed on production servers and this allows a consistent environment across live and work environments.
* requirements_dev.in - this lists the direct requirements the developers have when working on the app, but not for live environments. 
For example "pytest".  Usually there are no version locks specified, but sometimes a range is specified. 
This also usually includes "-r requirements.in" as the first line, so that all requirements are installed from one file.
* requirements_dev.txt - this lists all requirements developers have, with every one locked to one specific version. 
This allows a consistent environment between individual developers and between a developer and Travis.

Any process that updates these files correctly can be followed. The process is generally:

* Set up a clean virtual environment using your tool of choice
* pip install -r requirements.in
* pip freeze -r requirements.in > requirements.txt
* pip install -r requirements_dev.in
* cat requirements.in requirements_dev.in > requirements_combined_tmp.in
* pip freeze -r requirements_combined_tmp.in > requirements_dev.txt

There are then some cleanups needed to remove some things in the locked files that cause problems:

* sed -i 's/^-r.*//' requirements.txt requirements_dev.txt
* sed -i 's/pkg-resources==0.0.0//' requirements.txt requirements_dev.txt

Using the -r option to the freeze command means that the two locked files are in a consistent order. 
This means it is easy to compare changes between commits and see what libraries have had their versions upgraded and which haven't.

We do provide a handy script to update these files for you. You can run it with:

    curl https://raw.githubusercontent.com/open-contracting/standard-maintenance-scripts/master/scripts/update_requirements.sh | bash -

This assumes you want to use the virtualenv tool, and want to create a virtual environment called ".ve".

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
