# Known Issues — Review Index

This page is the short entry point. GitHub Issues remain the executable source of truth.

## P0

1. **Public repository environment hygiene**
   - Current source tree still tracks environment-configuration paths.
   - Secret values are intentionally not reproduced here.
   - The present task is not authorized to read or modify `.env` files.
   - See architecture Issue #1.

## Recently resolved

1. **Local / remote Git divergence**
   - Resolved through verified non-force history reconciliation.
   - See Issue #2.
2. **No fixed external-review SHA**
   - Resolved frozen functional baseline: `6989ed27c933716f9069bb9b14fba92624081fc4`.
   - See Issue #3.
3. **Tracked browser/test generated artifacts**
   - Current tree no longer contains tracked `.playwright-cli` artifacts or tokenizer Python bytecode.
4. **Python tokenizer clean-build reproducibility**
   - Resolved by source PR #30; see Issue #25.
5. **Registration password validation synchronization**
   - Resolved by source PR #31; see Issue #26.

## P1 / external gates

- Re-verify tokenizer runtime/fallback boundaries where later tokenizer code changes exceed the frozen functional baseline.
- Re-verify Android release/AAB/signing/Play readiness.
- Complete iOS macOS/Xcode/signing/device/TestFlight/App Store evidence.
- Audit mobile sync/offline queue/idempotency invariants.
- Assess CodeQL/code-scanning value for the actual supported languages in this monorepo.

## Product-quality follow-ups

- URL/email/path fragments should not become learnable vocabulary.
- fallback tokenization must preserve paragraph/section structure.
- Reader text needs semantic spaces, not visual spacing only.
- manual WordSense creation should not invent POS defaults.
- optional integrations should fail soft.
- duplicate lookup/network noise should be reduced only where current runtime evidence proves duplication.
