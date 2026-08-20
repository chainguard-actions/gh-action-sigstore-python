<!-- markdownlint-disable -->

# Hardening Report: sigstore--gh-action-sigstore-python/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **sigstore--gh-action-sigstore-python/v3.0.0** was hardened automatically. 7 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml uses tag-based (non-SHA) references for composite action steps: `uses: actions/upload-artifact@v4` and `uses: softprops/action-gh-release@v2`. These should be pinned to full 40-character commit SHAs to prevent supply-chain attacks.

Locations:

- `action.yml:97`
- `action.yml:103`

### unpinned-uses (severity: high)

.github/workflows/ci.yml uses tag-based (non-SHA) references: `uses: actions/checkout@v4` and `uses: actions/setup-python@v5`. These should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/ci.yml:12`
- `.github/workflows/ci.yml:13`

### unpinned-uses (severity: high)

.github/workflows/release.yml uses a tag-based (non-SHA) reference: `uses: actions/checkout@v4`. This should be pinned to a full 40-character commit SHA.

Locations:

- `.github/workflows/release.yml:16`

### unpinned-uses (severity: high)

.github/workflows/selftest.yml uses multiple tag-based (non-SHA) references: `actions/checkout@v4` (multiple steps), `actions/setup-python@v5` (multiple steps), and `actions/download-artifact@v4`. These should be pinned to full 40-character commit SHAs.

Locations:

- `.github/workflows/selftest.yml:27`
- `.github/workflows/selftest.yml:28`
- `.github/workflows/selftest.yml:47`
- `.github/workflows/selftest.yml:61`
- `.github/workflows/selftest.yml:62`
- `.github/workflows/selftest.yml:80`
- `.github/workflows/selftest.yml:97`
- `.github/workflows/selftest.yml:113`
- `.github/workflows/selftest.yml:126`
- `.github/workflows/selftest.yml:148`
- `.github/workflows/selftest.yml:176`
- `.github/workflows/selftest.yml:193`
- `.github/workflows/selftest.yml:200`
- `.github/workflows/selftest.yml:222`
- `.github/workflows/selftest.yml:258`

### unpinned-uses (severity: high)

.github/workflows/semgrep.yml uses a tag-based (non-SHA) reference: `uses: actions/checkout@v4`. This should be pinned to a full 40-character commit SHA.

Locations:

- `.github/workflows/semgrep.yml:19`

### missing-permissions (severity: medium)

.github/workflows/ci.yml has no top-level `permissions:` key and the single `lint` job also has no `permissions:` key. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions. A minimal `permissions: {}` or specific scopes should be declared.

Locations:

- `.github/workflows/ci.yml:1`

### missing-permissions (severity: medium)

.github/workflows/semgrep.yml has no top-level `permissions:` key and the `semgrep` job has no `permissions:` key. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions. A minimal `permissions: {}` or specific scopes should be declared.

Locations:

- `.github/workflows/semgrep.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action references by resolving them to full 40-character commit SHAs: actions/checkout@v4 → 11d5960a326750d5838078e36cf38b85af677262, actions/setup-python@v5 → a26af69be951a213d495a4c3e4e4022e16d87065, actions/upload-artifact@v4 → ea165f8d65b6e75b540449e92b4886f43607fa02, actions/download-artifact@v4 → d3f86a106a0bac45b974a628896c90dbdf5c8093, softprops/action-gh-release@v2 → 3bb12739c298aeb8a4eeaf626c5b8d85266b0e65. Added `permissions: {}` to ci.yml and semgrep.yml to enforce least-privilege. All 15 occurrences in selftest.yml were pinned. The only remaining tag-based reference is in README.md (documentation only).

