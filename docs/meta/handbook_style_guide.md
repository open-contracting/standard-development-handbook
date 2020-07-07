# Handbook style guide

Handbook contributors should follow this style guide.

## Links

When linking to a GiHub resource, use `HEAD` instead of a specific branch, tag or commit.

When linking to the standard's documentation, use the `latest` build instead of a specific version.

## Structure

Unless a page is short, it should start with a description of its contents.

If relevant, a page should include a section on **testing** that describes the tests to verify work.

## Admonitions

Admonitions (box outs) can be added using the **hint**, **note** and **warning** styles.

```eval_rst
.. hint::
   Use a hint admonition to share extra information that may be useful for a user of the documentation.
```

```eval_rst
.. note::
   Use a note admonition to indicate that there are areas where the documentation requires further improvement, but this does not block use of the current information.
```

```eval_rst
.. warning::
   Use a warning admonition to indicate that the documentation on a page may not accurately reflect current practice, or that substantial caveats exist that should be noted before following the documented process.
```

## Email addresses

If an email address is discoverable on Google, there is no use in simple obfuscations like [at] and [dot] that make the text less readable. If an email address is not yet public, it is best to keep it that way than to attempt obfuscation.
