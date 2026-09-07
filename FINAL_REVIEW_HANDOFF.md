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

6989ed27c933716f9069bb9b14fba92624081fc4

Why this SHA:
- Git history divergence had already been reconciled without force push.
- tracked Playwright/browser artifacts and tokenizer Python bytecode had been removed.
- source README and SECURITY policy had been added.
- GitHub workflow-token permissions were restricted to contents: read.
- source PR #25 merged the minimal Laravel Reverb Critical fix after A/B dependency/bootstrap validation.
- source PR #26 made the Web production image reproducible with a root lock file, `npm ci`, Docker build-context hygiene, and native `fsrs-rs-php`.
- real Chrome verification on the final production Web image completed Reader → lookup → save WordSense → sense ReviewCard → interval preview → rating with HTTP 200 responses and exactly one ReviewLog.
- the former Dependabot Critical advisory is fixed on this default-branch baseline.

This SHA is the current frozen application-code target for external review. Later source-master commits must be checked before assuming they are documentation-only.

Current source `master` also contains post-baseline fixes: source PR #30 made the Python tokenizer image reproducible, PR #31 fixed registration password-confirmation validation synchronization, PR #32 updated the targeted axios + moment browser runtime dependencies, and PR #34 added publication-state documentation. Publication status is synchronized through source merge commit `abba49dd9723170d861839b478dad9224505ea8c`; these later commits do not automatically inherit the frozen baseline's browser-acceptance scope.

## Product in one paragraph

LinguaCafe is being narrowed into an English reading-first learning product. A user reads real material, resolves the concrete meaning used in that sentence, keeps the source occurrence as evidence, and lets a sense-level ReviewCard use FSRS when natural reading does not provide enough repetition. ReviewLog records real ratings. AI is used mainly for explanation, translation, candidate generation and disambiguation; it should not fabricate formal review history.

## Platform status

### Web / PC
Most complete implementation. A live current-baseline Chrome regression is now recorded for login, Home, Library/import, Reader, dictionary lookup, WordSense creation, Vocabulary, sense Review and Settings. Fresh Docker verification also proved the final production Web image loads native `fsrs-rs-php`; interval preview and rating both returned HTTP 200. This does not by itself prove every admin/destructive path or production deployment topology.

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

Dependabot snapshot after source PR #26:
- 137 open alerts total;
- 0 Critical;
- 48 High;
- 73 Medium;
- 16 Low.

Manifest split:
- root package-lock.json: 46;
- composer.lock: 49;
- experimental resources/vue3/package-lock.json: 41;
- mobile/package-lock.json: 1.

The higher total follows the addition of the root package lock, which makes the previously unlocked root frontend dependency graph visible to Dependabot. Treat this as improved dependency visibility, not as proof that PR #26 introduced 24 new exploitable runtime vulnerabilities.

The former Critical Laravel Reverb advisory is fixed by merged source PR #25:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/25

The merged fix updates only Reverb v1.0.0 to v1.11.1 and ratchet/rfc6455 v0.3.1 to v0.4.1. Broad PR #24 was rejected because its wider dependency resolution broke Laravel 11.15 package discovery. Remaining advisories require separate reachability and compatibility decisions.

## Recently resolved post-baseline source fixes

- Architecture Issue #25 is resolved by source PR #30: the Python tokenizer image now uses a reproducible, pinned model-artifact path instead of depending on an unpinned live download during every clean build.
- Architecture Issue #26 is resolved by source PR #31: registration password-confirmation validation is synchronized in the client and was re-verified in real Chrome.
- Source PR #32 made targeted axios + moment runtime dependency updates. The remaining 137 Dependabot alerts still require separate production-reachability and compatibility triage.
- Source PR #34 added the publication-state documentation used to distinguish the frozen functional baseline from the newer default branch.

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
- 137 remaining Dependabot alerts are not 137 equally exposed production vulnerabilities.
- GitHub CodeQL success does not mean all findings are fixed.
- GitHub Stars, Product Hunt votes or download counts do not prove retention.
- file size alone does not justify refactoring.
- the experimental Vue3 directory is not the current Vue2 production frontend.

## Current decision state

The public external-review package is ready for review.

The product itself is not release-ready yet. Open environment-hygiene, remaining dependency/security triage, Android and iOS release gates, mobile sync/offline verification, production operations, and real-user validation remain intentionally visible. The Python tokenizer clean-build and registration-validation items are resolved post-baseline, and the Web/PC current-baseline Reader → WordSense → sense Review path is no longer an open browser-evidence gate.
