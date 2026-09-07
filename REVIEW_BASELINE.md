# External Review Baseline

Source repository:
https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local

Current review commit:
`190e7ab95e9415af23c9799cbc276714dcdd6ed5`

## What happened before this baseline

1. Local and remote Git histories had diverged.
2. The local-only `28c12d41` and remote `70a4a36f` were verified to have the same stable patch-id.
3. An isolated merge-tree completed without conflict and produced the same product tree as the pre-reconciliation remote.
4. A normal non-force push created the reconciliation history.
5. The source README was updated with the three-repository review entry.
6. Thirty-five tracked Playwright console/page artifacts and two Python bytecode files were removed.
7. Generic Python cache ignore rules were added.

## What this baseline proves

- external reviewers have one source SHA;
- the dirty local checkout was not bulk-published;
- the historical browser automation artifacts and tokenizer bytecode are absent from the current tree;
- the source repository links to the architecture and product-launch review repositories.

## What it does not prove

- tracked environment configuration is safe for public distribution;
- all local uncommitted assets have been classified;
- Web/PC current browser acceptance is complete;
- Android is Play Store ready;
- iOS is TestFlight/App Store ready.
