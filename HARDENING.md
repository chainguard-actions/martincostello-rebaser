<!-- markdownlint-disable -->

# Hardening Report: martincostello--rebaser/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **martincostello--rebaser/v3.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### broad-permissions (severity: medium)

The workflow file ossf-scorecard.yml has a top-level `permissions: read-all` which grants overly broad read access to all scopes. This should be replaced with specific minimal permissions scopes required by each job.

Locations:

- `.github/workflows/ossf-scorecard.yml:12`

## Iteration Notes

### Iteration 1

**Fixes applied:** broad-permissions

**Notes:**

Replaced the top-level `permissions: read-all` in ossf-scorecard.yml with specific minimal permissions: `contents: read` and `actions: read`. The job-level permissions block (`id-token: write`, `security-events: write`) was already correctly scoped and remains unchanged.

