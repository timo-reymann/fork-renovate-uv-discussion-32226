# 32226

First, read the [Renovate minimal reproduction instructions](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md).

Then replace the current `h1` with the Renovate Issue/Discussion number.

## Current behavior

Renovate uses the default pypi index, https://pypi.org/pypi/, for all defined packages in `pyproject.toml`. This fails because the package `my-sample-package-renovate` can't be found in pypi, because it's hosted at a custom index `https://my-private-index-url.com/simple`.


## Expected behavior

uv uses information from `tool.uv.index` in `pyproject.toml` to search in additional indices.

In this case for example we define the index `my-private-index` with the url `https://my-private-index-url.com/simple` and we've set it to `explicit=true`.

Additionally, we've set the index to `explicit=true` and used `tool.uv.sources` to define which packages use this index.

With that information Renovate should know that it should check `https://my-private-index-url.com/simple` for new versions of `my-sample-package-renovate`.

Additionally, if it's a private repo it should use the environment variables for verification called:
```
UV_INDEX_MY_PRIVATE_INDEX_USERNAME=...
UV_INDEX_MY_PRIVATE_INDEX_PASSWORD=...
```


## Link to the Renovate issue or Discussion

[Discussion #32226](https://github.com/renovatebot/renovate/discussions/32226)
