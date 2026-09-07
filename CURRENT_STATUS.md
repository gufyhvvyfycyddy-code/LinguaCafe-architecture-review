# Current Status — 2026-09-07

## Source / review baseline

- Source repository: `gufyhvvyfycyddy-code/LinguaCafe-local`
- Visibility: Public
- Frozen application-code review baseline: `bd95b6a8308de8e9663fab344c3ffccefa71e9d3`
- The earlier local/remote divergence has been reconciled.
- Tracked Playwright browser artifacts and tokenizer Python bytecode were removed before this baseline.
- GitHub workflow token permissions were restricted to `contents: read` at this baseline.
- Later source-master commits may contain review documentation only.
- The main local checkout still contains uncommitted user assets and has not been reset, cleaned, stashed, or bulk-published.

## Public security

Enabled on the public source repository:
- Secret Scanning;
- Push Protection;
- Dependabot vulnerability alerts;
- automated security fixes;
- Private Vulnerability Reporting;
- CodeQL default setup.

### P0 — environment hygiene

Tracked environment-configuration paths remain in the public source tree.

Current project rules did not authorize reading or modifying `.env` files. Secret values have not been copied into review documents.

Owner: architecture Issue #1.

### P0 — dependency security

Dependabot snapshot:
- total open alerts: 115;
- Critical: 1;
- High: 45;
- Moderate: 59;
- Low: 10.

Manifest split:
- `composer.lock`: 51;
- root `package.json`: 22;
- experimental `resources/vue3/package-lock.json`: 41;
- `mobile/package-lock.json`: 1.

The Critical affects the currently configured Laravel Reverb v1.0.0.

Scoped remediation candidate:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/24

PR #24 updates Reverb to v1.11.1 and related transitive dependencies. CodeQL checks pass, Composer PHP 8.2 dry-run passes with Windows-only pcntl/posix extension requirements ignored, and the new lock has no Critical Composer advisory. It is intentionally not auto-merged without application-level Linux regression evidence.

Owner: architecture Issue #23.

## CodeQL

The follow-up master scan after workflow-permission hardening completed successfully.

The three Actions missing-permissions findings were resolved.

Eight findings remain:
- `public/web.config`: missing X-Frame-Options — High;
- `public/js/dmak/raphael.js`: double escaping — High;
- three SenseReview test-only regex/sanitization findings — High;
- `tools/tokenizer.py`: two reflective-XSS findings — High;
- `tools/tokenizer.py`: exception-detail exposure — Medium.

These have not been dismissed merely to make the dashboard green.

Swift coverage is currently absent. The first Swift autobuild failed because fresh checkout lacked Capacitor packages under `mobile/node_modules`. Tracked in Issue #24.

## Platform

- Web/PC: implementation is the most complete; current-baseline real browser acceptance remains open.
- Android: native implementation exists; signed release/AAB/current Play readiness remains open.
- iOS: Xcode project and release materials exist; macOS/Xcode/signing/device/TestFlight/App Store evidence remains open.
