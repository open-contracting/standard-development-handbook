# Coding practices

* Instead of writing a 'TODO' in the code or documentation, create an issue on GitHub. TODO's in code are less visible to the rest of the team.

The [standard-maintenance-scripts](https://github.com/open-contracting/standard-maintenance-scripts) repository is used to enforce coding and formatting styles for Python, Markdown and JSON.

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
    json.dump(data, f, indent=2, separators=(',', ': '))
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
1. Run (replacing `path/to` twice with the output of `pwd` above):

        for i in *; if [ -d $i ]; cd $i; echo $i; path/to/bin/mdl --git-recurse --style path/to/mdlrc.rb .; cd ..; end; end

```eval_rst
.. toctree::
   :maxdepth: 2
   :glob:

   *

```
