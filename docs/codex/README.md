# Codex Handoff

## Purpose

This folder tracks repo-specific handoff notes for the CloakBrowser audit and follow-up maintenance work.

## Read Order

1. `AUDIT_LOG.md`
2. `SECURITY_NOTES.md`
3. `FEATURE_GAPS.md`
4. `TODO.md`
5. `PROJECT_MEMORY.md`

## Coding Style

- Keep Python and JS wrappers behaviorally aligned unless there is a platform-specific reason not to.
- Prefer small, explicit helper functions over hidden side effects in launch and download flows.
- Keep Windows, macOS, and Linux behavior covered in tests. Avoid Linux-only assertions in path and archive tests.
- Preserve safe defaults. Any opt-out like `CLOAKBROWSER_SKIP_CHECKSUM=true` must stay explicit and documented.

## Naming Style

- Reuse existing repo naming: `snake_case` for Python, `camelCase` for JS/TS, uppercase constants for platform and URL constants.
- Name test cases after behavior, not implementation details.
- When adding security helpers, name them after the decision they make, for example `is_windows_executable_path`.

## Logic Style

- Launch path: resolve config -> ensure binary -> build args -> launch browser/context -> patch humanize if requested.
- Download path: resolve version -> download to temp -> verify checksum -> extract safely -> flatten if needed -> mark executable -> optional background update.
- GeoIP path: do not block launch indefinitely. Time-bounded best effort only.

## Logging Points

- Binary download start, progress, checksum verification, extraction, and background update results.
- GeoIP timeout and fallback paths.
- `cloakserve` launch, seed reuse, CDP availability, and cleanup failures.

## Maintenance Rule

- Any code fix in wrapper, downloader, proxy, GeoIP, or `cloakserve` should update `AUDIT_LOG.md` and `TODO.md`.
