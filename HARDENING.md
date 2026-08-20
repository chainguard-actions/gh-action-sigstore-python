<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.1.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.1.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### github-env-injection (severity: high)

In the `selftest-identity-token` job's "Get OIDC token" step, the shell variable `identity_token` is populated by fetching from `$ACTIONS_ID_TOKEN_REQUEST_URL` (an inherited process env var not set in the same run block) via `curl | jq -r .value`, then written directly to `$GITHUB_OUTPUT` without the required sanitization step (`printf '%s' "$identity_token" | tr -d '\n\r'`). A malformed OIDC token response containing newline characters could inject arbitrary environment variables or outputs into subsequent steps.

Offending line: `echo "identity-token=$identity_token" >> $GITHUB_OUTPUT`

Locations:

- `.github/workflows/selftest.yml:12395`

## Iteration Notes

### Iteration 1

**Fixes applied:** github-env-injection

**Notes:**

Fixed the github-env-injection finding in hardened/action/.github/workflows/selftest.yml. In the `selftest-identity-token` job's 'Get OIDC token' step, added sanitization of the `identity_token` value before writing it to $GITHUB_OUTPUT. The fix introduces a `safe_identity_token` variable that strips newline and carriage return characters using `printf '%s' "$identity_token" | tr -d '\n\r'`, then writes the sanitized value to $GITHUB_OUTPUT instead of the raw token. Also quoted `"$GITHUB_OUTPUT"` for good shell hygiene.

