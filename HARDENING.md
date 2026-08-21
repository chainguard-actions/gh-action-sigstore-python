<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.0.1** was hardened automatically. 2 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `lint` job also has no job-level `permissions:` key. Without explicit permissions, the job inherits the default (potentially broad) repository permissions.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

The workflow file has no top-level `permissions:` key and the `semgrep` job also has no job-level `permissions:` key. Without explicit permissions, the job inherits the default (potentially broad) repository permissions.

Locations:

- `.github/workflows/semgrep.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** missing-permissions

**Notes:**

Added `permissions: {}` top-level blocks to both `.github/workflows/ci.yml` and `.github/workflows/semgrep.yml`. This explicitly sets all permissions to none, preventing the jobs from inheriting potentially broad default repository permissions. The lint job only runs `make lint` after checkout, and the semgrep job only runs `semgrep ci` using a secrets-based token — neither requires any GitHub API permissions.

### Iteration 2

**Fixes applied:** github-env-injection

**Notes:**

Fixed the github-env-injection finding in .github/workflows/selftest.yml at the selftest-identity-token job's 'Get OIDC token' step. The raw OIDC token fetched via curl | jq was being written directly to $GITHUB_OUTPUT without sanitization. Added `safe_token=$(printf '%s' "$identity_token" | tr -d '\n\r')` to strip embedded newlines/carriage returns, then used the sanitized value when writing to GITHUB_OUTPUT. Also properly quoted $GITHUB_OUTPUT as "$GITHUB_OUTPUT".

