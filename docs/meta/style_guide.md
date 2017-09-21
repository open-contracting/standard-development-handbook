# Handbook style guide

Handbook contributors should follow this style guide.

## Structure

Unless a page is short, it should start with a description of its contents.

If relevant, a page should include a section on **testing** that describes the tests to verify work.

## Admonitions

Admonitions (box outs) can be added using the **hint**, **note** and **warning** styles.

```eval_rst
  .. todo::
    Use a todo admonition to indicate issues that need to be addressed in updates to the documentation. Include a link to relevant GitHub issues using the : issue : ` nn ` syntax.
```

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
