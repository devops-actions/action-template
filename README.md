[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/devops-actions/action-template/badge)](https://api.securityscorecards.dev/projects/github.com/devops-actions/action-template)

# Action template

Template repo to get started with creating actions in the `devops-actions` organization. It contains the standard setup that every action repo in the org uses. Create a new repo from it with **Use this template**, then replace the placeholder `action.yml` and this README with your own action.

## Usage

```yaml
- uses: devops-actions/action-template@v1
  with:
    who-to-greet: 'Mona'
```

### Inputs

| Name | Required | Default | Description |
| --- | --- | --- | --- |
| `who-to-greet` | no | `World` | Who to greet |

### Outputs

| Name | Description |
| --- | --- |
| `greeting` | The greeting that was written to the log |

## What the template includes

All workflows call the shared reusable workflows in [devops-actions/.github](https://github.com/devops-actions/.github), pinned to a release SHA. Dependabot keeps those pins up to date.

| File | Purpose |
| --- | --- |
| `.github/workflows/ossf-scorecard.yml` | OpenSSF Scorecard analysis |
| `.github/workflows/issue-pr-tag.yml` | Tags the team in `vars.TAG_TEAM` on new issues and pull requests |
| `.github/workflows/approve-dependabot-pr.yml` | Approves and auto-merges Dependabot minor and patch updates |
| `.github/workflows/secure-inputs.yml` | Scans issues, pull requests and comments for injection attacks |
| `.github/workflows/dependency-review.yml` | Flags vulnerable dependencies in pull requests |
| `.github/workflows/actionlint.yml` | Lints the workflow files |
| `.github/workflows/actions-example-checker.yml` | Checks that the usage examples in the README match `action.yml` |
| `.github/workflows/actions-dependencies.yml` | Submits the actions used to the dependency graph |
| `.github/workflows/check-for-release.yml` | Opens an issue when there are unreleased changes |
| `.github/workflows/release.yml` | Publishes a release with SBOMs and attestations when a `v*` tag is pushed |
| `.github/dependabot.yml` | Monthly grouped updates for actions (npm and docker entries are commented out) |
| `.github/CODEOWNERS` | Requires review for workflow and AI instruction files |
| `LICENSE` | MIT |

The org variables `FIXED_ORG_NAME` and `TAG_TEAM` are already set at the organization level. Community health files (security policy, contributing guide, funding) are inherited from the org `.github` repo.

## After creating a repo from this template

A template doesn't copy repository settings, so set these on the new repo:

- **General**: enable *Allow auto-merge* and *Automatically delete head branches*.
- **Code security**: enable *Secret scanning* and *Push protection*.
- **Rules**: add a ruleset for `main` that requires a pull request and the checks of your build workflow. Give matrix jobs a stable name (for example `Build (${{ matrix.platform }})`) instead of the runner label, so a runner change doesn't break the ruleset.
- **Dependabot**: uncomment the npm or docker entry in `.github/dependabot.yml` if the action needs it.
