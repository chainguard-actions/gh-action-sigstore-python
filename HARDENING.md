# Hardening Report: sigstore--gh-action-sigstore-python/v3.0.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **sigstore--gh-action-sigstore-python/v3.0.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yml contains two `uses:` references pinned to mutable version tags rather than full 40-character commit SHAs. This exposes the action to supply-chain attacks if the upstream action tags are moved or compromised. Failing references: `actions/upload-artifact@v4` (line 98) and `softprops/action-gh-release@v2` (line 103).

Locations:

- `action.yml:98`
- `action.yml:103`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned both mutable tag references in action.yml to full 40-character commit SHAs: (1) actions/upload-artifact@v4 → @ea165f8d65b6e75b540449e92b4886f43607fa02 # v4 (line 98); (2) softprops/action-gh-release@v2 → @3bb12739c298aeb8a4eeaf626c5b8d85266b0e65 # v2 (line 103). Original tag names preserved as inline comments for readability.

