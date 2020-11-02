# Building the documentation

See the standard's page for [Building the documentation](../../../standard/technical/build).

## Change version of OCDS

1. Change `standard_tag` and `standard_version` in `conf.py` to the desired version of OCDS
1. Update the versions of extensions in `extension_versions.json`, if appropriate
1. [Rebuild the profile](#build-the-profile)

## Change extensions

To change the extensions in a profile, change `extension_versions.json`, then [rebuild the profile](#build-the-profile).

Extensions must be in the [extension registry](https://github.com/open-contracting/extension_registry) and should be tagged and released. See [creating new releases of core extensions](../../standard/technical/deployment.html#create-new-versions-of-core-extensions).

## Build the profile

See the [repository documentation](repository) for information on what files are built by `build-profile.py`.

```shell
make clean_dist
python schema/build-profile.py
```
