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

Current source `master` also contains post-baseline fixes through source merge commit `2abc82df754525c19733382200aaf72a930d436a`: PR #30 tokenizer image reproducibility, PR #31 registration validation, PR #32 targeted browser-runtime dependencies, PR #33 compatible PHP security refresh, PR #34/#35 publication synchronization, PR #36/#37 tokenizer/IIS CodeQL remediation, PR #39 unused Vue3 experiment removal, and PR #40 BrowserSync 3 development-tool update. These later commits do not automatically inherit the frozen baseline's browser-acceptance scope.

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
Architecture Issue #23 acceptance is satisfied.

Current Dependabot snapshot after source PR #40:
- 28 open alerts total;
- 0 Critical;
- 6 High;
- 18 Medium;
- 4 Low.

Manifest split:
- root `package-lock.json`: 24;
- `composer.lock`: 2;
- `docker/python/requirements.lock.txt`: 1;
- `mobile/package-lock.json`: 1;
- the experimental `resources/vue3/package-lock.json` was removed by PR #39.

Source PR #33 removed the compatible PHP advisories while preserving Laravel 11 behavior (Unit 745/745; Feature 2882/2882). PR #40 removed the old BrowserSync/localtunnel axios chain. The six remaining High alerts each have an explicit current non-reachability, accepted development-tool risk, or upgrade gate in `DEPENDENCY_HIGH_RISK_DISPOSITION_2026-09-07.md`.

Medium/Low dependency debt remains visible follow-up work. Laravel 12 and Vue3/Vuetify3 are planned platform migrations rather than hidden security-patch scope.

## Recently resolved post-baseline source fixes

- Architecture Issue #25 is resolved by source PR #30: the Python tokenizer image now uses a reproducible, pinned model-artifact path instead of depending on an unpinned live download during every clean build.
- Architecture Issue #26 is resolved by source PR #31: registration password-confirmation validation is synchronized in the client and was re-verified in real Chrome.
- Source PR #32 made targeted axios + moment runtime dependency updates.
- Source PR #34/#35 added and synchronized publication-state documentation.
- Source PR #33 completed the compatible PHP security refresh; PR #39 removed the unreferenced Vue3 prototype; PR #40 removed the old BrowserSync/localtunnel axios chain.
- Dependency High dispositions are recorded in `DEPENDENCY_HIGH_RISK_DISPOSITION_2026-09-07.md`.

## GitHub security status

Enabled:
- Secret Scanning;
- Push Protection;
- Dependabot vulnerability alerts;
- automated security fixes;
- Private Vulnerability Reporting;
- CodeQL default setup.

The workflow-token findings are fixed and current default-branch CodeQL has **0 open alerts**. Tokenizer boundary work is closed through source PR #36 / architecture Issue #28; IIS anti-clickjacking work is closed through source PR #37 / Issue #29; the legacy Raphaël finding is also fixed in the current default-branch scan.

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
- The 28 remaining Dependabot alerts are not equally exposed production vulnerabilities; the six High alerts have explicit dispositions and medium/low debt remains visible.
- Current default-branch CodeQL has zero open alerts, but this does not replace runtime/platform security testing.
- GitHub Stars, Product Hunt votes or download counts do not prove retention.
- file size alone does not justify refactoring.
- the former experimental Vue3 directory was not part of the Vue2 production frontend and was removed by source PR #39.

## Current decision state

The public external-review package is ready for review.

The product itself is not release-ready yet. Public environment hygiene, Android and iOS release gates, mobile sync/offline verification, production operations, privacy/support and real-user validation remain intentionally visible. The dependency P0 and current CodeQL findings have been reduced to evidence-backed dispositions/zero-open status; medium/low dependency debt and Laravel12/Vue3 modernization remain follow-up work.
