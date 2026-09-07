# Current Status — 2026-09-07

## Source / review baseline

- Source repository: gufyhvvyfycyddy-code/LinguaCafe-local
- Visibility: Public
- Frozen application-code review baseline: bbfd3426e089008fb19e5920850e4b9c4bda5ab8
- Earlier local/remote divergence has been reconciled without force push.
- Tracked Playwright browser artifacts and tokenizer Python bytecode were removed.
- GitHub workflow token permissions are explicitly restricted to contents: read.
- The baseline includes the merged minimal Laravel Reverb Critical remediation from source PR #25.
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

Current default-branch Dependabot snapshot after source PR #25:
- total open alerts: 113;
- Critical: 0;
- High: 44;
- Moderate: 59;
- Low: 10.

Manifest split:
- composer.lock: 49;
- root package.json: 22;
- experimental resources/vue3/package-lock.json: 41;
- mobile/package-lock.json: 1.

The former Critical Laravel Reverb advisory is fixed on default branch by source PR #25:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/25

The merged fix is intentionally minimal: Reverb v1.0.0 to v1.11.1 and ratchet/rfc6455 v0.3.1 to v0.4.1. Broad PR #24 was rejected because its Symfony 7.4 resolution broke Laravel 11.15 package discovery in A/B validation.

The remaining 113 alerts require production-reachability and compatibility triage. They must not be bulk-upgraded as one dependency migration.

Owner: architecture Issue #23.

## CodeQL

The workflow-permission findings are fixed.

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

- Web/PC: implementation is the most complete; current-baseline real browser acceptance remains open until a live browser run is recorded.
- Android: native implementation exists; signed release/AAB/current Play readiness remains open.
- iOS: Xcode project and release materials exist; macOS/Xcode/signing/device/TestFlight/App Store evidence remains open.

## Review package

The three public repositories are ready to inspect. Release readiness is not claimed while the open environment-hygiene, dependency, browser, Android and iOS gates remain visible.
