# Feature Gaps

## High Priority

### 1. First-party regression harness for detection claims

- The repo has strong human-facing proof, but no automated smoke suite that regularly checks a small, stable set of public detection pages.
- Add a maintainer-only smoke target that records result snapshots and compares wrapper behavior across Python and JS.

### 2. Signed update manifest for binary discovery

- Checksum verification exists, but release discovery still trusts remote metadata from GitHub Releases.
- Add a signed release manifest or detached signatures for binary version metadata to reduce update-chain trust on metadata endpoints.

### 3. Shared archive safety invariants between Python and JS

- Python and JS wrappers now both have archive safety logic, but they still implement it separately.
- Add shared archive test vectors and keep both stacks pinned to the same safety cases.

## Medium Priority

### 4. Better Windows-native ZIP extraction path

- Current JS path still depends on PowerShell being present.
- A future improvement is to replace that shell-out path with a pure Node or direct .NET-hosted approach.

### 5. Offline or locked-down mode

- Add an explicit mode that disables background update checks and optional GeoIP fetches for controlled environments.
- This would help CI, regulated networks, and reproducible internal deployments.

### 6. Mirror-aware trust policy

- `CLOAKBROWSER_DOWNLOAD_URL` disables GitHub fallback, but trust behavior is still mostly implicit.
- Add documented mirror policy modes: strict mirror only, official fallback allowed, and offline only.
