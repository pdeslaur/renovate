# renovate

Runs [Renovate](https://docs.renovatebot.com/) on a schedule against the
repositories listed in [the workflow](.github/workflows/renovate.yml)'s matrix.

Each job authenticates with [octo-sts](https://github.com/octo-sts/app)
instead of a personal access token. octo-sts exchanges the job's GitHub
Actions OIDC token for a GitHub App token scoped to one repository, if that
repository's `.github/chainguard/renovate.sts.yaml` trust policy allows it.

[`config.json5`](config.json5) holds the configuration every repository
gets. A repository can override it with its own `renovate.json`.

## Adding a repository

1. Install the octo-sts GitHub App on the repository.
2. Copy [`.github/chainguard/renovate.sts.yaml`](.github/chainguard/renovate.sts.yaml)
   into the repository and merge it to its default branch.
3. Add the repository to the workflow's matrix.

To run Renovate now, start the workflow by hand:

```sh
gh workflow run renovate.yml -R pdeslaur/renovate -f log-level=debug
```
