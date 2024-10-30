# 32226

First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.

## Current behavior

Renovate uses the default pypi index, https://pypi.org/pypi/, for all defined packages in `pyproject.toml`.
This fails because the package `renovate-sample-library-32226` can't be found in pypi, because it's hosted at a custom index `https://dl.cloudsmith.io/public/my-renovate-example-org/open-source-renovate-sample-library-32226/python/simple/`.


## Expected behavior

uv uses information from `tool.uv.index` in `pyproject.toml` to search in additional indices.

In this case for example we define the index `cloudsmith-os-index` with the url `https://dl.cloudsmith.io/public/my-renovate-example-org/open-source-renovate-sample-library-32226/python/simple/`.

We've set the index to `explicit=true` and used `tool.uv.sources` to define which packages use this index.

With that information Renovate should know that it should check `https://dl.cloudsmith.io/public/my-renovate-example-org/open-source-renovate-sample-library-32226/python/simple/` for new versions of `cloudsmith-os-index`.

If it's a private repo it should use the environment variables for verification called:
```
UV_INDEX_CLOUDSMITH_OS_INDEX_USERNAME=...
UV_INDEX_CLOUDSMITH_OS_INDEX_PASSWORD=...
```

## Link to the Renovate issue or Discussion

[Discussion #32226](https://github.com/renovatebot/renovate/discussions/32226)
