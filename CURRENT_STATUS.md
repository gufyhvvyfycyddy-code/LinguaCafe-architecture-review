# Current Status — 2026-09-07

## Git / publication

- Source repository: `gufyhvvyfycyddy-code/LinguaCafe-local`
- Visibility: Public
- Current external-review baseline: `190e7ab95e9415af23c9799cbc276714dcdd6ed5`
- The earlier local/remote divergence has been reconciled.
- The reconciliation itself changed Git history only; the later publication-hygiene commit removed tracked browser automation artifacts and Python bytecode, plus added generic Python cache ignore rules.
- The main local checkout still contains uncommitted user assets and has not been reset, cleaned, stashed, or bulk-published.

## Public security

GitHub Secret Scanning and Push Protection are enabled on all three public repositories.

The source repository no longer tracks the historical `.playwright-cli` artifacts or tokenizer `__pycache__` files on the current baseline.

Remaining P0:
- tracked environment configuration paths are still present in the public source tree;
- current project rules prohibit this task from reading or modifying `.env` files, so that part is deliberately left unresolved and must be handled through a separately authorized credential-safe cleanup.

Status: `PARTIAL — P0 ENV HYGIENE BLOCKED`.

## Platform

- Web/PC: implementation is the most complete; current-baseline browser acceptance still needed.
- Android: implementation exists; current release/AAB/signing/Play readiness still needs proof.
- iOS: implementation/release materials exist; macOS/Xcode/signing/device/TestFlight/App Store evidence remains incomplete.
