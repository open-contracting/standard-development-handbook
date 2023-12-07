Deploying the documentation
===========================

A profile's deployment is the same as the standard's :doc:`../../standard/technical/deployment`, except where noted below. If a profile is unversioned, some of the below may be irrelevant.

Perform maintenance tasks
-------------------------

Check the profile's individual handbook page for any maintenance tasks.

Version the profile
-------------------

If this is the first numbered version of a profile, in its ``docs/_templates/layout.html``, add (substituting ``{root}`` with ``ppp``, for example):

.. code-block:: jinja

   {% block version_options %}
   <!--#include virtual="/includes/version-options-profiles-{root}.html" -->
   {% endblock %}

Update the changelog
--------------------

Update the profile's changelog (if any) with links to its extensions' changelogs.

Review the pull requests since the last release. To review the commits that are not part of a pull request (using the fish shell):

.. code-block:: fish

   git show (git rev-list --first-parent --no-merges 1.0-dev --since=2019-10-21)

To review the messages only (using the fish shell):

.. code-block:: fish

   git show --oneline -s (git rev-list --first-parent --no-merges 1.0-dev --since=2019-10-21)

Replace the branch (``1.0-dev``) and date (``2019-10-21``) as needed.
