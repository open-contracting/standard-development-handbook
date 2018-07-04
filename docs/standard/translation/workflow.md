# Translation workflow

For the specific steps that each role follows in Transifex, see the [steps for each role](../using_transifex#steps-for-each-role).

1. The Release Manager freezes source strings, i.e. no pull requests will be merged that change English strings in Markdown, JSON, CSV or  `.po` files.
1. The Coordinator recruits people into the roles of translator, proofreader and reviewer and [gives access to the Transifex project](../using_transifex#controlling-access-permissions).
1. The Coordinator sends translators the links to the Transifex project and to this documentation page.
1. When a Translator completes the translation of at least half the untranslated words, they contact the Proofreader with a link to the resource.
1. When a Proofreader completes the proofreading of at least half the unreviewed strings, they contact the Reviewer with a link to the resource.
1. Once a Reviewer has reviewed all unreviewed strings for all resources, they contact the Coordinator.

The **Release Manager** is the person responsible for the deployment of the new release of OCDS. The role of **Coordinator** is comparable to that in the [terminology process](../terminology#coordinator).
