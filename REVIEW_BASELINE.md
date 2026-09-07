# External Review Baseline

Source repository:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local

Frozen application-code review commit:

`bd95b6a8308de8e9663fab344c3ffccefa71e9d3`

## Why this baseline

Before this SHA:

1. local and remote Git histories were reconciled without force push;
2. the duplicate-equivalent local/remote fix was verified by stable patch-id;
3. tracked Playwright console/page artifacts were removed;
4. tracked tokenizer Python bytecode was removed;
5. generic Python cache ignore rules were added;
6. the source repository gained the three-repository review entry and security reporting policy;
7. GitHub workflow-token permissions were restricted to `contents: read`;
8. the follow-up master CodeQL run completed successfully.

## What this baseline proves

- reviewers have one stable application-code SHA;
- the dirty local checkout was not bulk-published;
- known generated browser/Python artifacts are absent from the current tree;
- source, architecture review and product-launch repositories are linked;
- workflow-token hardening is present.

## What it does not prove

- tracked environment configuration is safe for public distribution;
- dependency vulnerabilities are resolved;
- all local uncommitted assets have been classified;
- Web/PC current real-browser acceptance is complete;
- Android is Play Store ready;
- iOS is TestFlight/App Store ready;
- Swift CodeQL coverage is currently complete.

## Security candidate branch

Laravel Reverb Critical remediation is under review in source PR #24:

https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local/pull/24

Do not treat that PR as merged baseline until application-level regression evidence exists.
