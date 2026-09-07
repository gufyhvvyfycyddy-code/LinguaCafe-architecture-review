# Current Status — 2026-09-07

## Source / review baseline

- Source repository: gufyhvvyfycyddy-code/LinguaCafe-local
- Visibility: Public
- Frozen application-code review baseline: 6989ed27c933716f9069bb9b14fba92624081fc4
- Earlier local/remote divergence has been reconciled without force push.
- Tracked Playwright browser artifacts and tokenizer Python bytecode were removed.
- GitHub workflow token permissions are explicitly restricted to contents: read.
- The baseline includes the merged minimal Laravel Reverb Critical remediation from source PR #25 and the reproducible Web/native-FSRS production-image remediation from source PR #26.
- Post-baseline current-source fixes include PR #30 (reproducible Python tokenizer image), PR #31 (registration password-confirmation validation synchronization), PR #32 (targeted browser runtime dependencies), PR #33 (compatible PHP security refresh), PR #34/#35 (publication-state synchronization), PR #36/#37 (tokenizer and IIS CodeQL fixes), PR #39 (unused Vue3 experiment removal), and PR #40 (BrowserSync 3 development-tool update).
- Current review status is synchronized through source merge commit `2abc82df754525c19733382200aaf72a930d436a`.
- Architecture Issues #25, #26, #28 and #29 are resolved.
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

Current default-branch Dependabot snapshot after source PR #40:
- total open alerts: 28;
- Critical: 0;
- High: 6;
- Medium: 18;
- Low: 4.

Manifest split:
- root `package-lock.json`: 24;
- `composer.lock`: 2;
- `docker/python/requirements.lock.txt`: 1;
- `mobile/package-lock.json`: 1;
- the experimental `resources/vue3/package-lock.json` was removed by source PR #39.

Source PR #33 reduced PHP advisories while preserving Laravel 11 compatibility; A/B testing showed Carbon 3.13.2 changed the existing DST/local-midnight queue-order behavior, so the accepted lock keeps Carbon 3.8.4 while retaining the security fixes. Unit 745/745 and Feature 2882/2882 passed on the final lock.

Source PR #40 upgraded BrowserSync to 3.0.4, removing the old development `localtunnel -> axios 0.21.4` chain. Source PR #39 removed the unreferenced Vue3 prototype and its 41 experimental alerts.

The six remaining High alerts have explicit dispositions in `DEPENDENCY_HIGH_RISK_DISPOSITION_2026-09-07.md`: current non-reachability/accepted development-tool risk for the present product path, plus explicit Laravel 12 / Vue3 migration gates where required.

Architecture Issue #23 acceptance criteria are satisfied and the issue can close as a P0 launch blocker. Medium/Low dependency debt remains follow-up work.

## CodeQL

Current default-branch CodeQL has **0 open alerts**.

- source PR #36 hardened tokenizer JSON/output and exception boundaries; architecture Issue #28 is closed;
- source PR #37 added the IIS anti-clickjacking header; architecture Issue #29 is closed;
- the legacy Raphaël double-escaping finding is also fixed in the current default-branch scan;
- configured Actions, C#, Java/Kotlin, JavaScript/TypeScript and Python analyses are green on the recent security/dependency PRs.

Swift CodeQL coverage is currently absent. The first Swift autobuild failed because a fresh checkout did not have required Capacitor packages under mobile/node_modules. Tracked in Issue #24.

Owner: architecture Issue #19 and Issue #24.

## Platform

- Web/PC: current-baseline real Chrome acceptance is recorded for login, Home, Library/import, Reader, dictionary lookup, WordSense creation, Vocabulary, sense Review and Settings. The final production Web image loaded native `fsrs-rs-php`; interval preview and rating returned HTTP 200 and the smoke card produced exactly one ReviewLog.
- Android: native implementation exists; signed release/AAB/current Play readiness remains open.
- iOS: Xcode project and release materials exist; macOS/Xcode/signing/device/TestFlight/App Store evidence remains open.

## Review package

The three public repositories are ready to inspect. Release readiness is not claimed while environment hygiene, Android signed release/AAB/Play evidence, iOS bootstrap/signing/TestFlight/App Store evidence, mobile sync/offline verification, production operations, privacy/support and real-user deployment gates remain open.

Recently resolved post-baseline source items include tokenizer reproducibility (#25 / PR #30), registration validation (#26 / PR #31), tokenizer/IIS CodeQL findings (#28/#29 / PR #36/#37), compatible PHP security refresh (PR #33), unused Vue3 dependency debt (PR #39), and the old BrowserSync/localtunnel axios chain (PR #40).
