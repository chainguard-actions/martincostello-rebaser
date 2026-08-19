<!-- markdownlint-disable -->

# Hardening Report: martincostello--rebaser/v3.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **martincostello--rebaser/v3.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

build.yml contains a `uses:` reference to a Docker image pinned by tag+SHA256 digest rather than a 40-character git commit SHA. The reference `uses: docker://rhysd/actionlint:1.7.12@sha256:b1934ee5f1c509618f2508e6eb47ee0d3520686341fec936f3b79331f9315667` has a ref after `@` of `sha256:b1934ee5f1c509618f2508e6eb47ee0d3520686341fec936f3b79331f9315667`, which is not a 40-character lowercase hex git commit SHA as required by the pinning check.

Locations:

- `.github/workflows/build.yml:105`

### broad-permissions (severity: medium)

ossf-scorecard.yml sets `permissions: read-all` at the top level, granting overly broad read access to all scopes. This should be replaced with specific minimal permissions (e.g., `contents: read`, `security-events: write`, `id-token: write`) rather than the blanket `read-all` grant. (Note: the file contains a `# zizmor: ignore[excessive-permissions]` comment acknowledging this, but it remains a security finding per the check rules.)

Locations:

- `.github/workflows/ossf-scorecard.yml:11`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions

**Notes:**

1. Fixed unpinned-uses in build.yml: Replaced `uses: docker://rhysd/actionlint:1.7.12@sha256:b1934ee5f1c509618f2508e6eb47ee0d3520686341fec936f3b79331f9315667` with `uses: rhysd/actionlint@914e7df21a07ef503a81201c76d2b11c789d3fca # v1.7.12` — a proper 40-character git commit SHA reference resolved via lookup_action_sha for the v1.7.12 tag.
2. Fixed broad-permissions in ossf-scorecard.yml: Replaced `permissions: read-all` with `permissions:
  contents: read` — the minimal top-level permission needed. The job-level permissions block already grants the specific `id-token: write` and `security-events: write` permissions needed by the OSSF Scorecard action.

