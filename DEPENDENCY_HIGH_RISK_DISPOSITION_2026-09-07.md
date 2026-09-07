# Dependency High-Risk Disposition — 2026-09-07

Source of truth: `gufyhvvyfycyddy-code/LinguaCafe-local`

Current source checkpoint after the compatible PHP refresh, unused Vue3 removal and BrowserSync 3 update:
`2abc82df754525c19733382200aaf72a930d436a`

## Current Dependabot snapshot

- Open alerts: 28
- Critical: 0
- High: 6
- Medium: 18
- Low: 4

Manifest split:

- `composer.lock`: 2 (1 High, 1 Medium)
- `docker/python/requirements.lock.txt`: 1 High
- root `package-lock.json`: 24 (4 High, 16 Medium, 4 Low)
- `mobile/package-lock.json`: 1 Medium
- `resources/vue3/package-lock.json`: removed with source PR #39; its 41 experimental alerts are no longer in the default-branch dependency graph

Source PR #33 reduced PHP advisories while preserving Laravel 11 compatibility. Source PR #40 removed the old BrowserSync -> localtunnel -> axios 0.21.4 development chain.

## Remaining High dispositions

### 1. Laravel framework — GHSA-5vg9-5847-vvmq

Status: **current default product path is not reachable; upgrade gate remains**.

- Current Laravel line is 11.x. The upstream fixed line begins at Laravel 12.60.0.
- The advisory requires a user-controlled email address to reach an outbound-mail flow.
- LinguaCafe's active public user creation route is `/users/create`; it validates and stores email but does not send email.
- Password-reset and email-verification routes in `routes/auth.php` are commented out.
- `User` does not implement `MustVerifyEmail`.
- Repository search found no active application mail-send path besides the inactive password-reset controller; the Horizon mail route is commented out.

Decision: do not cross the Laravel major boundary as part of a dependency patch. Before any user-controlled outbound email flow is enabled, require either Laravel >=12.60.0 or an explicit CR/LF rejection/sanitization boundary plus dedicated security tests.

### 2. NLTK — GHSA-8mgp-746c-j5xp

Status: **evidence-backed non-reachability; upstream patch unavailable**.

- Locked NLTK is 3.10.3 and the advisory currently has no patched version.
- The advisory concerns model import/export APIs that accept caller-controlled file paths.
- LinguaCafe source does not import or call NLTK directly.
- NLTK is present through `newspaper3k`; LinguaCafe calls `Article(url)`, `download()`, `parse()` and reads `article.text`.
- No vulnerable model persistence/import/export API is called by the current tokenizer service.

Decision: retain the package while the current call graph remains unchanged, monitor the upstream advisory, and re-open this disposition if direct NLTK model-path APIs are introduced.

### 3. Vuetify 2 — GHSA-3jp5-5f8r-q2wg

Status: **current exploit precondition is not present; migration required as platform debt**.

- Current shipped frontend uses Vuetify 2.7.2.
- The advisory affects the preset configuration merge path and has no Vuetify 2 fix; the patched line is Vuetify 3.
- `resources/js/vuetify.js` constructs Vuetify from repository-controlled local options/themes.
- No Vuetify preset configuration fed by user/network input was found in the current source.

Decision: current product path does not expose the malicious-preset precondition. Do not force a Vuetify 3 migration inside a security patch. Track Vue2/Vuetify2 retirement as a planned frontend-platform migration and re-open as P0 if user-controlled preset/config injection is introduced.

### 4–5. PostCSS — GHSA-r28c-9q8g-f849 and GHSA-6g55-p6wh-862q

Status: **build-time only; no untrusted CSS build input**.

- Root PostCSS resolves to a patched 8.5.x line.
- The vulnerable PostCSS 7 instances remain nested under legacy Vue2/Laravel-Mix build tooling such as `@vue/component-compiler-utils` and `resolve-url-loader`.
- These packages execute while compiling repository-controlled Vue/Sass/CSS sources.
- No runtime route passes uploaded/user-controlled CSS into this build pipeline.

Decision: treat as build-tool debt, not a shipped runtime High. Remove during the Vue2/Laravel-Mix modernization rather than forcing incompatible transitive overrides.

### 6. Immutable.js — GHSA-v56q-mh7h-f735

Status: **local development tooling only**.

- The vulnerable Immutable 3.8.4 instance is an internal dependency of BrowserSync 3.
- BrowserSync is used by the Laravel Mix development/live-reload configuration.
- It is not imported by the shipped application source.
- Forcing Immutable across a major boundary inside BrowserSync is not accepted without upstream compatibility evidence.

Decision: accepted development-tool risk. Replace/remove BrowserSync during frontend-tooling modernization if upstream does not move to a patched Immutable line.

## Acceptance against architecture Issue #23

1. Critical production advisories: **0**.
2. Every remaining High has an explicit fix, upgrade gate, or evidence-backed non-reachability/accepted-risk decision above.
3. Experimental Vue3 dependency debt is removed from the current source tree by source PR #39.
4. Dependency changes preserve current behavior:
   - source PR #33: Unit 745/745 and Feature 2882/2882 passed after Carbon was held at 3.8.4 following A/B timezone testing;
   - source PR #39: root `npm ci` and production build passed after removing the unreferenced Vue3 prototype;
   - source PR #40: BrowserSync 3 production build passed and the old localtunnel/axios chain disappeared.

Issue #23 can therefore close as a P0 launch blocker. Medium/Low dependency debt and the planned Laravel 12 / Vue3 migration remain visible follow-up work.
