# Final External Review Handoff — 2026-09-07

This is the shortest entry point for an external reviewer.

## Three public repositories

1. Source of truth
   https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local

2. Architecture / technical debt / UI-UX / platform review
   https://github.com/gufyhvvyfycyddy-code/LinguaCafe-architecture-review

3. Product launch / hosting / app stores / growth / commercial review
   https://github.com/gufyhvvyfycyddy-code/LinguaCafe-product-launch

## Frozen application-code review baseline

Use:

bbfd3426e089008fb19e5920850e4b9c4bda5ab8

Why this SHA:
- Git history divergence had already been reconciled without force push.
- tracked Playwright/browser artifacts and tokenizer Python bytecode had been removed.
- source README and SECURITY policy had been added.
- GitHub workflow-token permissions were restricted to contents: read.
- source PR #25 merged the minimal Laravel Reverb Critical fix after A/B dependency/bootstrap validation.
- the former Dependabot Critical advisory is fixed on this default-branch baseline.

This SHA is the current frozen application-code target for external review. Later source-master commits must be checked before assuming they are documentation-only.

## Product in one paragraph

LinguaCafe is being narrowed into an English reading-first learning product. A user reads real material, resolves the concrete meaning used in that sentence, keeps the source occurrence as evidence, and lets a sense-level ReviewCard use FSRS when natural reading does not provide enough repetition. ReviewLog records real ratings. AI is used mainly for explanation, translation, candidate generation and disambiguation; it should not fabricate formal review history.

## Platform status

### Web / PC
Most complete implementation. Historical acceptance evidence exists, but a live current-baseline browser regression still needs to be recorded before release readiness is claimed.

### Android
Native project exists and historical emulator evidence exists. Current signed release artifact / AAB / Play Console readiness is not yet proven.

### iOS
Native Xcode project and release materials exist. Final macOS/Xcode/signing/device/TestFlight/App Store evidence is not complete.

Fresh GitHub CodeQL exposed a reproducibility gap: Swift autobuild failed because Capacitor packages expected under mobile/node_modules were absent on a fresh checkout. This is tracked in architecture Issue #24.

## Highest-priority blockers

### P0 — Public repository environment hygiene
Architecture Issue #1.

The current public source tree still tracks environment-configuration paths. Secret values are intentionally not reproduced in review documents. Current project rules do not authorize reading or modifying .env files, so this remains explicitly unresolved.

### Dependency security
Architecture Issue #23.

Dependabot snapshot after source PR #25:
- 113 open alerts total;
- 0 Critical;
- 44 High;
- 59 Moderate;
- 10 Low.

Manifest split:
- composer.lock: 49;
- root package.json: 22;
- experimental resources/vue3/package-lock.json: 41;
- mobile/package-lock.json: 1.

The former Critical Laravel Reverb advisory is fixed by merged source PR #25:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/25

The merged fix updates only Reverb v1.0.0 to v1.11.1 and ratchet/rfc6455 v0.3.1 to v0.4.1. Broad PR #24 was rejected because its wider dependency resolution broke Laravel 11.15 package discovery. Remaining advisories require separate reachability and compatibility decisions.

## GitHub security status

Enabled:
- Secret Scanning;
- Push Protection;
- Dependabot vulnerability alerts;
- automated security fixes;
- Private Vulnerability Reporting;
- CodeQL default setup.

The three CodeQL workflow-token findings were fixed on master.

Eight CodeQL findings remain on the current default branch:
- IIS public/web.config: missing X-Frame-Options;
- bundled third-party public/js/dmak/raphael.js: double escaping;
- three test-only SenseReview regex/sanitization findings;
- tools/tokenizer.py: two reflective-XSS findings;
- tools/tokenizer.py: one exception-detail exposure finding.

These are intentionally not dismissed merely to make the dashboard green. The Raphaël asset is still loaded by the user layout; production Docker networking keeps the tokenizer service internal, but its endpoint findings still need call-path review.

## Architecture questions worth reviewing first

1. Does Reader keep display logic separate from formal learning mutations?
2. Is there exactly one formal path that writes ReviewLog / changes FSRS?
3. Are mobile retry/offline operations truly idempotent?
4. Are legacy word-review paths still required by active users/data?
5. Does tokenizer fallback preserve paragraph and section structure?
6. Are URL/email/path fragments excluded from learnable vocabulary?
7. Which large modules have mixed ownership versus simply many lines?
8. Can the iOS project be bootstrapped reproducibly from a clean checkout?
9. Which dependency advisories affect shipped paths versus experiments/dev tooling?
10. Can current non-English legacy assets such as DMAK be removed from the English-only runtime without breaking required compatibility?

## Product / launch questions worth reviewing first

1. Who should be the first 10 deep-use users?
2. Should the first public release prioritize Web + Android before iOS?
3. Which hosting region best matches the initial users and compliance path?
4. What is the minimum reliable server/backup/email/monitoring setup?
5. Which distribution channel can produce retained users, not just impressions?
6. What must be measured before charging money?
7. What user evidence should exist before speaking to investors?

## How to use the repositories

- README = navigation.
- docs = deep evidence and research.
- GitHub Issues = executable problems.
- ADR/accepted project docs = stable decisions.
- source commit = code truth.
- old reports = historical evidence only.

## What the reviewer should not assume

- App Store is not completed.
- Play Store is not completed.
- 113 remaining Dependabot alerts are not 113 equally exposed production vulnerabilities.
- GitHub CodeQL success does not mean all findings are fixed.
- GitHub Stars, Product Hunt votes or download counts do not prove retention.
- file size alone does not justify refactoring.
- the experimental Vue3 directory is not the current Vue2 production frontend.

## Current decision state

The public external-review package is ready for review.

The product itself is not release-ready yet. Open environment-hygiene, dependency, browser, Android and iOS gates are intentionally visible rather than hidden.
