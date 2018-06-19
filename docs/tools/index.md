# Tools and resources

* The [OCDS validator](http://standard.open-contracting.org/validator/) is a deployment of [CoVE (GitHub)](https://github.com/OpenDataServices/cove) to convert between spreadsheet and JSON representations of OCDS data, and to validate against the standard.
* [OCDS Data](https://github.com/open-contracting/ocdsdata) is a tool for downloading and analyzing OCDS data.
* [OCDS Kit](https://pypi.org/project/ocdskit/) is a suite of command-line tools for working with OCDS data.
* [ocds-faker](https://github.com/open-contracting/ocds-faker) is a command-line tool to generate clearly fake data for OCDS release packages, for testing.
* [ocds-merge](https://github.com/open-contracting/ocds-merge) is a Python library that provides functions to merge a list of OCDS releases into a `compiledRelease` or a `versionedRelease`, for creating an OCDS record.
* [ocds-show](https://github.com/open-contracting/ocds-show) is a JavaScript application to visualize OCDS releases and records, to allow easier comprehension of OCDS data.
* [ocds-show-ppp](https://github.com/open-contracting/ocds-show-ppp) is an instance of OCDS Show configured for the [PPP profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) of OCDS.
* [sample-data](https://github.com/open-contracting/sample-data) contains a selection of sample data that can help demonstrate what OCDS data looks like.

For tools relating to extensions, see [extensions tools](../extensions#tools). For guidance on using the [standard extension template](https://github.com/open-contracting/standard_extension_template) in particular, see [creating extensions](../extensions#creating-extensions).

## Priority tech support

Priority is assessed based on the impact of the project becoming unavailable and the degree of usage :issue:`76`, which can be assessed based on [Python package downloads](http://www.pypi-stats.com/author/?q=30327), [GitHub traffic](https://github.com/open-contracting/standard-development-handbook/issues/76#issuecomment-334540063) and user feedback.

### Critical

* `standard`: core documentation
* `OpenDataServices/cove`: critical step in implementation journey

### High

* Profiles
* Core extensions
* `ocds-merge`: reference implementation for merging releases
* `extension_registry`: integrates with `standard`
* `documentation-support`: dependency of `standard`
* `sphinxcontrib-opencontracting`: dependency of `standard`
* `standard_theme`: dependency of `standard`
* `OpenDataServices/sphinxcontrib-jsonschema`: dependency of `standard`
* `OpenDataServices/sphinxcontrib-opendataservices`: dependency of `standard`
* `extension_registry.py`: common dependency

### Medium

* Community extensions
* `sample-data`: key resource, frequently visited
* `standard_extension_template`: key resource
* `glossary`: potential future key resource
* `ocdsdata`: key tool
* `ocdskit`: key tool
* `standard-maintenance-scripts`: internal, quality assurance
* `standard-development-handbook`: internal, key documentation

### Low

* `api-specification`: draft
* `extension_creator`
* `json-schema-random`
* `ocds-faker`
* `ocds-show`
* `ocds-show-ppp`
* `ocds_profile_template`: internal template
* `standard-legacy-staticsites`: for older versions of documentation
* `open-contracting.github.io`: redirects to `standard`

## OCDS extension support

If changes are made to the behavior of extensions in OCDS, the following tools may need to be updated, in addition to the [extensions tools](../extensions#tools):

* [CoVE](https://github.com/OpenDataServices/cove)
* [ocdskit](https://github.com/open-contracting/ocdskit) `mapping-sheet` and `tabulate` commands
* [ocds-faker](https://github.com/open-contracting/ocds-faker)
* [ocds-merge](https://github.com/open-contracting/ocds-merge)
* [ocds-show](https://github.com/open-contracting/ocds-show)
* [ocds-show-ppp](https://github.com/open-contracting/ocds-show-ppp)

## Adding tools to the OGP Toolbox

From December 2016 - June 2018 we maintained a list of Open Contracting tools in the OGP Toolbox [Open Contracting Tools collection](https://ogptoolbox.org/en/collections/10). 

From June 2018, we maintain a tool directory using AirTable, and helpdesk team members should consult the "Internal Process: Learning log and tools directory" document for details. 

## Adding tools to the OCP Resources

Resources we want to highlight are added to the [OCP Resources](https://www.open-contracting.org/data-standard/tools/) page.

1. Request a login for [open-contracting.org](https://www.open-contracting.org/) from Georg Neumann, OCP Communications Manager
1. [Login](https://www.open-contracting.org/wp-admin/)
1. Click "Resources" > "Add resource" from the sidebar
1. Enter a title, short description and long description
1. Select values for:
    * Audience
    * Author
    * Organisation ("Open Contracting Partnership")
    * Issue (blank)
    * Resource Type (one of "Data tool", "Guide", "Training Material")
    * Country and Region ("International", or "Latin America and the Caribbean" for Spanish resources)
    * Open Contracting ("Data standard" and, if a "Data tool", "Implementation")
1. Enter a URL for "Link". If it a Google Drive file or folder, make sure its name is tagged as "#public" and that it's shared as "Anyone with the link can view". See the caveats about the format of Google Drive URLs in the bitly.com instructions below.
1. Click "preview" to check the information you have entered
1. Click "Save as draft" and ask Georg to review and publish the draft resource

If the link is to a Google Drive file or folder, use a Bit.ly link to track clicks:

1. Login to [bitly.com](https://bitly.com) with the @OpenContracting Twitter account
1. Click "Create BitLink"
1. Paste the link to the Google Drive file or folder. Omit `?ts=…`, `?usp=sharing`, `#heading=…`, `/u/0`, `/a/open-contracting.org`, etc. The URL should look like one of:
    * `https://docs.google.com/document/d/{id}/edit`
    * `https://docs.google.com/presentation/d/{id}/edit`
    * `https://docs.google.com/spreadsheets/d/{id}/copy`
    * `https://docs.google.com/spreadsheets/d/{id}/edit#gid={gid}`
    * `https://drive.google.com/drive/folders/{id}`
    * `https://drive.google.com/file/d/{id}/view`
    * `https://drive.google.com/open?id={id}`
1. Edit the short URL. Start with the file or folder's name, omit conjunctions and hashtags, replace spaces with hyphens, and, if appropriate, prefix "OCDS-" and suffix the OCDS version (e.g. `-v11`) and language code (e.g. `-fr`). For example, "Releases and Records Exercise (OCDS 1.1) #public" becomes "OCDS-Releases-Records-Exercise-v11".
1. Add the "OCDS" tag
1. Click "Save"
