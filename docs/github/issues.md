# Issues

Issues requesting updates to the standard are handled as documented in the [revision process](http://standard.open-contracting.org/latest/en/support/governance/#revision-process).

## Managing long issues

Some issues produce long discussions, and the original intent of the issue may change over time; this can make it more difficult to catch up on the current state of the issue. To deal with this, the issue's description should be edited to reflect the current state of the issue, summarize the discussion so far, and link to the most recent comment from which the discussion may continue.

Restarting the discussion with a new issue causes the following problems:

* Old participants aren't notified of activity on the new issue, and need to subscribe to it.
* New participants need to read all issues referencing the new issue to rebuild the context.
* If the old issue is closed in favor of a new issue, and the new issue is thereafter not resolved but is closed (for whatever reason, like insufficient demand), a reader of the old issue may assume that the new issue is either open or resolved. They would need to follow the chain to realize that it's unresolved and closed, before adding a comment to say, "I need this."

## Automatically closing issues through pull requests

When creating a pull request that fixes one or more issues, add the text "fixes #42" or "closes #42" in the pull request's description so that GitHub [automatically closes the issues when the pull request is merged](https://help.github.com/articles/closing-issues-using-keywords/).

## Manually closing issues

All issues should be closed with a brief rationale. This comment makes it easy to understand what happened and affords participants an opportunity to engage with the rationale. Examples of simple rationales are:

* "Resolved in the above commit" if there's a commit referencing the issue that appears nearby
* "Resolved in the [name] extension" with a link to the extension that was created
* "Closing, because [explanation]"
