# Tools and resources

* The [OCDS validator](http://standard.open-contracting.org/validator/) is a deployment of [CoVE (GitHub)](https://github.com/OpenDataServices/cove) to convert between spreadsheet and JSON representations of OCDS data, and to validate against the standard. 
* [mapping-sheet-generator](https://github.com/open-contracting/mapping-sheet-generator) generates a flattened representation of an OCDS schema. 
* [ocds-faker](https://github.com/open-contracting/ocds-faker) is a command-line tool to generate clearly fake data for OCDS release packages, for testing. 
* [ocds-merge](https://github.com/open-contracting/ocds-merge) is a Python library that provides functions to merge a list of OCDS releases into a `compiledRelease` or a `versionedRelease`, for creating an OCDS record. 
* [ocds-show](https://github.com/open-contracting/ocds-show) is a JavaScript application to visualize OCDS releases and records, to allow easier comprehension of OCDS data. 
* [ocds-show-ppp](https://github.com/open-contracting/ocds-show-ppp) is an instance of OCDS Show configured for the [PPP profile](http://standard.open-contracting.org/profiles/ppp/latest/en/) of OCDS.
* [ocds-tabulate](https://github.com/open-contracting/ocds-tabulate) is a Python script to convert OCDS data into tabular form, for importing into a relational database.
* [sample-data](https://github.com/open-contracting/sample-data) contains a selection of sample data that can help demonstrate what OCDS data looks like. 

For tools relating to extensions, see [extensions tools](../extensions#tools). For guidance on using the [standard extension template](https://github.com/open-contracting/standard_extension_template) in particular, see [creating extensions](../extensions#creating-extensions).

## OCDS extension support

If changes are made to the behavior of extensions in OCDS, the following tools may need to be updated:

* [CoVE](https://github.com/OpenDataServices/cove)
* [flatten-tool](https://github.com/opendataservices/flatten-tool/)
* [mapping-sheet-generator](https://github.com/open-contracting/mapping-sheet-generator)
* [ocds-faker](https://github.com/open-contracting/ocds-faker)
* [ocds-show](https://github.com/open-contracting/ocds-show)
* [ocds-show-ppp](https://github.com/open-contracting/ocds-show-ppp)
* [ocds-tabulate](https://github.com/open-contracting/ocds-tabulate)

## Adding tools to the OGP Toolbox

The [OGP Toolbox](https://ogptoolbox.org/) has a collection of [Open Contracting Tools](https://ogptoolbox.org/en/collections/10).

"Reusable tools, applications and processes that consume OCDS data" (from OCP's objectives) are added to the OGP Toolbox.

1. [Login](https://crm.open-contracting.org/projects/ocds/wiki/Logins#OGP-Toolbox)
1. Create a [new tool](https://ogptoolbox.org/en/tools/new) in the toolbox
1. Fill in at least the Name, Description, Logo and Website fields
1. Copy the tool's link
1. Edit the [Open Contracting Tools](https://ogptoolbox.org/en/collections/10/edit) collection
1. Scroll to the bottom of the page and paste the tool's link into the "Add a tool" field
1. Click the "Publish Your Collection" button

## Adding tools to the OCP Resources

Resources we want to highlight are added to the [OCP Resources](https://www.open-contracting.org/data-standard/tools/) page.

1. Request a login for [open-contracting.org](https://www.open-contracting.org/) from Georg Neumann, OCP Communications Manager
1. [Login](https://www.open-contracting.org/wp-admin/)
1. Select "Resources" from the sidebar
1. Click "Add resource"
1. Enter a title, short description and long description for your resource
1. Select appropriate values from the dropdown boxes for audience, author, organization, issue, etc.
1. Paste a link to the resource into the "link" section, making sure the resource has appropriate sharing settings and is tagged as "#public"
1. Click "preview" to check the information you have entered
1. Click "Save as draft" and ask Georg to review and publish the draft resource
