# Download and bundle devstats data

This action downloads devstats for one or more GitHub repositories,
and uploads the result as an artifact.

## Example

```yaml
name: Query devstats

on:
  push:
    branches:
      - main
      - v*

jobs:
  devstats-query:
    runs-on: ubuntu-latest
    steps:
      - uses: stefanv/devstats-download-action@main
        with:
          repos: |
            - yourname/reponame
            - yourname/reponame-2
          artifact-name: devstats-yourname
```

The above would produce an artifact named `devstats-yourname.zip`, containing (with today's date) `2024-11-14-devstats-reponame.tar.xz` and `2024-11-14-devstats-reponame-2.tar.xz`.

By default, we use the GitHub-provisioned token, but you may need to set one manually if you're hitting rate limits:

```yaml
      - uses: stefanv/devstats-download-action@main
        with:
          token: ${{ secrets.GRAPHQL_API_TOKEN }}
```

The token is a "personal access token" created at
https://github.com/settings/tokens?type=beta.  It does not need any
permissions. Set up the token as `GRAPHQL_API_TOKEN` at
https://github.com/your-org/your-repo/settings/secrets/actions.
