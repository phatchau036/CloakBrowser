# Audit Log

## 2026-05-12

### Scope

- Clone upstream `CloakHQ/CloakBrowser`
- Audit wrapper quality, feature gaps, test health, release hygiene, and security posture
- Prepare a public, maintainable fork candidate

### Initial Findings

- Python baseline: `pytest tests -v -m "not slow"` failed 11 cases on Windows.
- JS baseline: `npm.cmd test` failed 5 cases.
- `npm.cmd audit` reported 12 vulnerabilities, including high severity findings in `tar` and dev dependency chains.
- README release banner is stale: root README still says `Latest: v0.3.26`, while package versions are `0.3.28`.

### Root Causes Seen Early

- Test expectations still assume `.tar.gz` or POSIX-style separators in Windows runs.
- Python `_is_executable()` uses `os.access(..., X_OK)`, which is not a reliable executable signal on Windows.
- JS Windows ZIP extraction shells out to PowerShell with inline string interpolation, which is fragile and potentially unsafe when paths contain quotes.
- Archive extraction hardening in JS depends partly on a vulnerable `tar` version and does not validate link targets as strictly as the Python extractor path.

### Expected Fix Areas

- Cross-platform tests
- Windows executable detection
- Safer ZIP extraction argument passing on Windows
- Tar dependency and extraction hardening
- Release/docs consistency

### Final Result

- Python non-slow suite: `405 passed, 1 skipped, 36 deselected`
- JS build: passed
- JS tests: `324 passed, 11 skipped`
- `npm audit`: `0 vulnerabilities`

### Remaining Constraint

- Public forking of the wrapper code is fine.
- Public redistribution of the upstream compiled binary is not fine under `BINARY-LICENSE.md` without separate permission.
