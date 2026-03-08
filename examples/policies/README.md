# Example Policies

Readiness policies customize which criteria are evaluated and how they are scored. These examples are meant to show three common ways to tailor a readiness report:

- narrow the report to a specific concern
- exclude checks that do not apply to your repository
- raise the quality bar for teams that want stricter gating

## Usage

Pass a policy file with `--policy` using a relative `./` path:

```sh
agentrc readiness --policy ./examples/policies/ai-only.json
agentrc readiness --policy ./examples/policies/strict.json
```

Multiple policies can be chained (comma-separated):

```sh
agentrc readiness --policy ./examples/policies/ai-only.json,./my-overrides.json
```

When policies are chained, later policies can further disable checks or override metadata from earlier ones. A common pattern is to start with a broad baseline policy and then layer a small repo-specific override on top.

## Included Policies

| File                    | Purpose                                                                                                 |
| ----------------------- | ------------------------------------------------------------------------------------------------------- |
| `ai-only.json`          | Disables repo-health criteria so the report focuses on AI tooling readiness                             |
| `repo-health-only.json` | Disables AI-tooling criteria and the `agents-doc` extra so the report focuses on core repository health |
| `strict.json`           | Sets a 100% pass-rate threshold and raises the impact of selected criteria                              |

## Choosing a policy

Use `ai-only.json` when you want to measure how ready a repository is for AI-assisted development without mixing in general engineering hygiene.

Use `repo-health-only.json` when you want a traditional repository-quality pass that ignores AI-specific setup.

Use `strict.json` when you want the default readiness model but with no partial credit on the overall threshold and stronger weighting on selected checks.
