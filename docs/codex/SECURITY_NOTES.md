# Security Notes

## Current High-Signal Risks

### 1. JS archive extraction dependency risk

- `js/package-lock.json` currently pulls a vulnerable `tar` release.
- Even with checksum verification enabled by default, the code supports checksum opt-out and fallback conditions.
- Mitigation direction: bump `tar`, tighten extraction validation, and keep checksum verification on by default.

### 2. Windows PowerShell extraction quoting

- `js/src/download.ts` interpolates archive and destination paths into a PowerShell command string.
- A path containing `'` can break the command and creates an unnecessary injection surface.
- Mitigation direction: pass archive and destination as positional arguments to a script block instead of string interpolation.

### 3. Binary redistribution licensing

- Wrapper source is MIT, but `BINARY-LICENSE.md` restricts redistribution of the compiled Chromium binary.
- A public fork can publish wrapper code, docs, and tests, but must not re-host or redistribute upstream binary assets without a separate license.

## Lower-Severity or Deferred Items

- Dev-only dependency vulnerabilities in test tooling may still require major-version upgrades and revalidation.
- GeoIP lookups must remain bounded to avoid turning proxy failures into a launch-time denial of service.
