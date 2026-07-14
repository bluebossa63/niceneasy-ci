# niceneasy-ci

Shared **reusable GitHub Actions workflows** for the nice'n'easy agent ecosystem.

This repository is intentionally public so that private repositories in the
account can consume its reusable workflows without extra Actions access
configuration.

## `node-ci.yml`

A generic Node/TypeScript CI job. Steps run in a fixed order and are skipped when
their command input is empty: `install → precheck → lint → build → test`.

### Usage

```yaml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

jobs:
  ci:
    uses: bluebossa63/niceneasy-ci/.github/workflows/node-ci.yml@main
    with:
      node-version: "22"
      working-directory: "."
      build-command: "npm run build"
      test-command: "npm test"
```

### Inputs

| Input | Default | Purpose |
|-------|---------|---------|
| `node-version` | `"22"` | Node.js version |
| `working-directory` | `"."` | Run dir (monorepo subdir support) |
| `install-command` | `"npm ci"` | Dependency install |
| `precheck-command` | `""` | Optional pre-lint check (e.g. type-check) |
| `lint-command` | `""` | Optional lint |
| `build-command` | `""` | Optional build |
| `test-command` | `""` | Optional test |

Empty command inputs skip their step.
