# Project Memory

## Repository Shape

- Python package at `cloakbrowser/`
- JS package at `js/`
- `bin/cloakserve` is a Python CDP multiplexer entrypoint
- Tests are substantial in both ecosystems and are worth treating as first-class product surface

## Important Constraints

- Python and JS wrappers intentionally mirror each other
- Binary version can differ by platform during rollout windows
- Public forking is constrained by `BINARY-LICENSE.md`

## Audit Snapshot

- Date: 2026-05-12
- Baseline Python test result: 11 failures on Windows, mostly path/archive expectation drift plus timeout behavior
- Baseline JS test result: 5 failures, mostly outdated asset-extension expectations
- Final Python result: 405 passed, 1 skipped, 36 deselected
- Final JS result: build passed, 324 passed, 11 skipped
- Final security snapshot: `npm audit` clean after dependency and extraction hardening
