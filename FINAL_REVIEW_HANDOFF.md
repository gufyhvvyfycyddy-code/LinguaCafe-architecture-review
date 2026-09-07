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

`bd95b6a8308de8e9663fab344c3ffccefa71e9d3`

Why this SHA:
- Git history divergence had already been reconciled.
- tracked Playwright/browser artifacts and tokenizer Python bytecode had been removed before this point.
- the source README and SECURITY policy had been added.
- GitHub workflow token permissions were explicitly restricted to `contents: read`.
- the master CodeQL run for this SHA completed successfully.

Later source-master commits may be documentation-only. Reviewers can use this SHA when they need one stable application-code target.

## Product in one paragraph

LinguaCafe is being narrowed into an English reading-first learning product. A user reads real material, resolves the concrete meaning used in that sentence, keeps the source occurrence as evidence, and lets a sense-level ReviewCard use FSRS when natural reading does not provide enough repetition. ReviewLog records real ratings. AI is used mainly for explanation, translation, candidate generation and disambiguation; it should not fabricate formal review history.

## Platform status

### Web / PC
Most complete implementation. Historical acceptance evidence exists, but current-baseline real browser regression remains open.

### Android
Native project exists and historical emulator evidence exists. Current signed release artifact / AAB / Play Console readiness is not yet proven.

### iOS
Native Xcode project and release materials exist. Final macOS/Xcode/signing/device/TestFlight/App Store evidence is not complete.

Fresh GitHub CodeQL also exposed a reproducibility gap: Swift autobuild failed because Capacitor packages expected under `mobile/node_modules` were absent on a fresh checkout. This is tracked in architecture Issue #24.

## Highest-priority blockers

### P0 — Public repository environment hygiene
Architecture Issue #1.

The current public source tree still tracks environment-configuration paths. Secret values are intentionally not reproduced in review documents. Current project rules did not authorize reading or modifying `.env` files, so this remains explicitly unresolved.

### P0 — Production dependency security
Architecture Issue #23.

Dependabot snapshot on 2026-09-07:
- 115 open alerts total;
- 1 Critical;
- 45 High;
- 59 Moderate;
- 10 Low.

Manifest split:
- `composer.lock`: 51;
- root `package.json`: 22;
- experimental `resources/vue3/package-lock.json`: 41;
- `mobile/package-lock.json`: 1.

The only Critical is current-runtime Laravel Reverb v1.0.0. A bounded remediation PR is open:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/24

The PR updates Reverb to v1.11.1 and related transitive packages. It is intentionally not auto-merged because it still needs application-level Linux regression evidence.

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
- IIS `public/web.config`: missing X-Frame-Options;
- bundled third-party `public/js/dmak/raphael.js`: double escaping;
- three test-only SenseReview regex/sanitization findings;
- `tools/tokenizer.py`: two reflective-XSS findings;
- `tools/tokenizer.py`: one exception-detail exposure finding.

These have not been dismissed merely to make the dashboard green.

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
- 115 Dependabot alerts are not 115 equally exposed production vulnerabilities.
- GitHub CodeQL success does not mean all findings are fixed.
- GitHub Stars, Product Hunt votes or download counts do not prove retention.
- file size alone does not justify refactoring.
- the experimental Vue3 directory is not the current Vue2 production frontend.

## Current decision state

The public external-review package is ready for review.

The product itself is not release-ready yet. The open P0s and platform gates above are intentionally visible rather than hidden.
