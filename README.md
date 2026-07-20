# FinaticORG shared GitHub config

Canonical Dependabot templates and reusable security workflows for FinaticORG repositories.

## Dependabot templates

Copy from `dependabot-templates/` into each repo’s `.github/dependabot.yml`:

| Template | Repos |
| --- | --- |
| `npm.yml` | FinaticWeb, FinaticConnect, FinaticClientSDK, FinaticServerSDK-Node, FinaticTester |
| `pip.yml` | FinaticAPI, FinaticCore, FinaticBackground, FinaticServerSDK-Python, FinaticMTConnector |
| `finatic-orchestrator.yml` | Finatic |
| `demoapps-multi.yml` | FinaticDemoApps |
| `terraform-infra.yml` | Infra |
| `actions-only.yml` | Database, `.github` |

All templates: weekly schedule, `target-branch: develop`, assignees/reviewers `founders`, grouped minor/patch.

## Reusable security workflows

Call from each repo’s `.github/workflows/security.yml` (see `security-templates/`):

```yaml
jobs:
  actionlint:
    uses: FinaticORG/.github/.github/workflows/reusable-actionlint.yml@main
```

Workflows pin `@main`. Promote changes: `develop` → `staging` → `main`.
