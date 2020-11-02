Markdown linting
================

To perform periodic Markdown linting, you must:

1. Install `Markdownlint <https://github.com/markdownlint/markdownlint>`__:

   ::

       bundle init
       bundle add mdl

2. Create ``~/.config/mdl/style.rb``:

   ::

       all

       # Rules can be configured. See https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md

       # See https://github.com/markdownlint/markdownlint/blob/master/docs/RULES.md#md026---trailing-punctuation-in-header
       rule 'MD026', :punctuation => '.,;:!'

       exclude_rule 'MD009' # Trailing spaces (common error frustrates users)
       exclude_rule 'MD013' # Line length (breaking lines in paragraphs produces longer diffs)
       exclude_rule 'MD033' # Inline HTML (some files require HTML)

3. Change into a directory containing local copies of GitHub repositories, and run (using the fish shell):

   ::

       for i in *; if [ -d $i ]; cd $i; echo $i; bundle exec mdl --git-recurse --style ~/.config/mdl/style.rb .; cd ..; end; end
