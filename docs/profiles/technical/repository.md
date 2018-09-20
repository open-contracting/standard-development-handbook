# Profile repository

## Branches and tags

If a profile hasn't yet adopted a versioning scheme, see the general [branch management](../../../github/branch_management) page.

If a profile has adopted a versioning scheme, see the standard's page for [branches and tags](../../../standard/technical/repository#branches-and-tags). The only difference is that a profile's tag names use dots (`1.0.0`) instead of double underscores (`1__0__0`).

## Structure

Profiles follow a similar [structure](../../../standard/technical/repository#structure) to the standard's, with fewer nesting directories, i.e.:

* `docs` instead of `standard/docs/en`
* `locale` instead of `standard/locale`
* `schema` instead of `standard/schema`

The [`schema/build-profile.py`](https://github.com/open-contracting/standard_profile_template/blob/master/schema/build-profile.py) script calls the [`build_profile` method](https://github.com/open-contracting/documentation-support/blob/master/ocdsdocumentationsupport/__init__.py) in `documentation-support`, which compiles a profile's extensions into a consolidated extension, storing the results in `schema/profile`, and extends OCDS with the consolidated extension, storing the results in `schema/patched`. It also copies the extensions' documentation into the profile and updates the `codelists` field in `extension.json`. All these built files are version controlled.

Note that, once built, the contents of `schema/profile` are copied to the root of built documentation, via `html_extra_path` in `conf.py`.
