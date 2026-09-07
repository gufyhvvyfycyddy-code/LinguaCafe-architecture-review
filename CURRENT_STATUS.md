# Current Status — 2026-09-07

## Source / review baseline

- Source repository: gufyhvvyfycyddy-code/LinguaCafe-local
- Visibility: Public
- Frozen application-code review baseline: 6989ed27c933716f9069bb9b14fba92624081fc4
- Earlier local/remote divergence has been reconciled without force push.
- Tracked Playwright browser artifacts and tokenizer Python bytecode were removed.
- GitHub workflow token permissions are explicitly restricted to contents: read.
- The baseline includes the merged minimal Laravel Reverb Critical remediation from source PR #25 and the reproducible Web/native-FSRS production-image remediation from source PR #26.
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

Current project rules do not authorize reading or modifying .env files. Secret values have not been copied into review documents.

Owner: architecture Issue #1.

### Dependency security

Current default-branch Dependabot snapshot after source PR #26:
- total open alerts: 137;
- Critical: 0;
- High: 48;
- Medium: 73;
- Low: 16.

Manifest split:
- root package-lock.json: 46;
- composer.lock: 49;
- experimental resources/vue3/package-lock.json: 41;
- mobile/package-lock.json: 1.

The increase from the earlier 113-alert snapshot follows the addition of the root lock file: GitHub can now enumerate the root frontend dependency graph that was previously not locked in the source tree. This is increased visibility, not evidence that PR #26 itself introduced 24 new exploitable runtime vulnerabilities.

The former Critical Laravel Reverb advisory is fixed on default branch by source PR #25:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/25

The merged fix is intentionally minimal: Reverb v1.0.0 to v1.11.1 and ratchet/rfc6455 v0.3.1 to v0.4.1. Broad PR #24 was rejected because its Symfony 7.4 resolution broke Laravel 11.15 package discovery in A/B validation.

The remaining 137 alerts require production-reachability and compatibility triage. They must not be bulk-upgraded as one dependency migration.

Owner: architecture Issue #23.

## CodeQL

The workflow-permission findings are fixed. Source PR #26 passed the configured CodeQL checks for Actions, C#, Java/Kotlin, JavaScript/TypeScript and Python.

Eight findings remain on the current default branch:
- public/web.config: missing X-Frame-Options — High;
- public/js/dmak/raphael.js: double escaping — High;
- three SenseReview test-only regex/sanitization findings — High;
- tools/tokenizer.py: two reflective-XSS findings — High;
- tools/tokenizer.py: exception-detail exposure — Medium.

The Raphaël file is still loaded by the current user layout through legacy DMAK assets, so it is not dismissed as dead code. The tokenizer service is internal-only in production Docker networking, but its findings still require endpoint/call-path review before dismissal.

Swift CodeQL coverage is currently absent. The first Swift autobuild failed because a fresh checkout did not have required Capacitor packages under mobile/node_modules. Tracked in Issue #24.

Owner: architecture Issue #19 and Issue #24.

## Platform

- Web/PC: current-baseline real Chrome acceptance is recorded for login, Home, Library/import, Reader, dictionary lookup, WordSense creation, Vocabulary, sense Review and Settings. The final production Web image loaded native `fsrs-rs-php`; interval preview and rating returned HTTP 200 and the smoke card produced exactly one ReviewLog.
- Android: native implementation exists; signed release/AAB/current Play readiness remains open.
- iOS: Xcode project and release materials exist; macOS/Xcode/signing/device/TestFlight/App Store evidence remains open.

## Review package

The three public repositories are ready to inspect. Release readiness is not claimed while the open environment-hygiene, dependency, Python-tokenizer clean-build, Android and iOS gates remain visible. Registration validation UX is separately tracked as Issue #26.
