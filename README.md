# thesaladetheory/.github

Organisation-wide defaults for The Salade Theory: reusable GitHub Actions workflows (and, later, `SECURITY.md`, `CONTRIBUTING.md` and issue/PR templates).

This repository is **public** so that every repo in the org can call its workflows. Never put secrets, internal URLs or customer data here.

## Reusable workflows

| Workflow                        | What it does                                                                                                                                                             |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `.github/workflows/node-ci.yml` | `npm ci`, `prettier --check`, then Nx targets (default `lint,typecheck,test,build`). Pull requests run `nx affected`; pushes to `main` and manual runs check everything. |

Call it from a repo with a thin workflow, pinned to a full commit SHA (the org requires SHA pinning):

```yaml
jobs:
  ci:
    uses: thesaladetheory/.github/.github/workflows/node-ci.yml@<commit-sha>
```

Rules for changes here:

- Every `uses:` is pinned to a full commit SHA with the version in a comment.
- `GITHUB_TOKEN` is read-only by default; a job asks for more only when it needs it.
- Inputs reach shell scripts through `env:`, never by `${{ }}` inside `run:` (script injection).
