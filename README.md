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

All templates: weekly schedule, `target-branch: develop`, `open-pull-requests-limit: 2`, assignees/reviewers `founders`, grouped minor/patch.

## Security templates (cost controls)

Copy from `security-templates/` into each repo’s `.github/workflows/security.yml`:

| Template | Repos |
| --- | --- |
| `security-python.yml` | FinaticAPI, FinaticCore, FinaticBackground, FinaticServerSDK-Python, FinaticMTConnector |
| `security-npm.yml` | FinaticWeb, FinaticConnect, FinaticClientSDK, FinaticServerSDK-Node |
| `security-tester.yml` | FinaticTester |
| `security-orchestrator.yml` | Finatic |
| `security-demoapps.yml` | FinaticDemoApps |
| `security-infra.yml` | Infra |
| `security-actions-only.yml` | Database, `.github` |

**Trigger / job policy (all templates):**

- **PR:** `actionlint` + `gitleaks` only
- **Weekly schedule / `workflow_dispatch` / push to `main`:** also `osv`, licenses, CodeQL (where configured)
- **No** push triggers on `develop` / `staging` (avoids merge double-runs)
- Skip `dependabot[bot]`; `concurrency` cancels superseded runs on the same ref

Reusable workflows pin `@main`. Promote changes: `develop` → `staging` → `main`.

```yaml
jobs:
  actionlint:
    uses: FinaticORG/.github/.github/workflows/reusable-actionlint.yml@main
```
