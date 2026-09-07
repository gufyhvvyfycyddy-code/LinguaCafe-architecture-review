# External Review Baseline

Source repository:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local

Frozen application-code review commit:

bbfd3426e089008fb19e5920850e4b9c4bda5ab8

## Why this baseline

Before or at this SHA:

1. local and remote Git histories were reconciled without force push;
2. duplicate-equivalent local/remote changes were checked before convergence;
3. tracked Playwright console/page artifacts were removed;
4. tracked tokenizer Python bytecode was removed;
5. generic Python cache ignore rules were added;
6. the source repository gained the three-repository review entry and security reporting policy;
7. GitHub workflow-token permissions were restricted to contents: read;
8. CodeQL default setup completed on the supported non-Swift languages;
9. source PR #25 merged the minimal Laravel Reverb Critical fix after A/B dependency/bootstrap validation.

## Merged Critical dependency remediation

Source PR #25:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/25

The merged change updates Laravel Reverb v1.0.0 to v1.11.1 and ratchet/rfc6455 v0.3.1 to v0.4.1. The earlier broad PR #24 was rejected because its Symfony 7.4 resolution broke Laravel 11.15 package discovery in A/B validation.

Independent validation on the minimal candidate established:
- PHP 8.2 dependency installation succeeds;
- Laravel package discovery succeeds;
- Artisan bootstrap succeeds;
- Composer audit reports no Critical advisory for Reverb or RFC6455;
- the default-branch Dependabot Critical count became zero after merge.

## What this baseline proves

- reviewers have one stable application-code SHA;
- the dirty local checkout was not bulk-published;
- known generated browser/Python artifacts are absent from the current tree;
- source, architecture-review and product-launch repositories are linked;
- workflow-token hardening is present;
- the previously identified Reverb Critical advisory is not present on this baseline.

## What it does not prove

- tracked environment configuration is safe for public distribution;
- all remaining dependency advisories are resolved;
- all local uncommitted assets have been classified;
- Web/PC current real-browser acceptance is complete;
- Android is Play Store ready;
- iOS is TestFlight/App Store ready;
- Swift CodeQL coverage is complete.
