# Optimization Directions

这是给外部审查者的排序，不是要求一次性重构全仓。

## 1. Public hygiene

当前最高风险：
- 环境配置仍被 Git 跟踪；
- 需要单独授权的 secret/credential-safe cleanup。

已完成：
- Secret Scanning；
- Push Protection；
- Dependabot vulnerability alerts；
- automated security fixes；
- CodeQL default setup；
- 移除 tracked Playwright 产物；
- 移除 tracked Python bytecode。

## 2. Freeze and test the real baseline

当前 source baseline：
190e7ab95e9415af23c9799cbc276714dcdd6ed5

下一步不是继续加功能，而是重新验：
- Web main journey；
- tokenizer；
- Reader；
- Sense Review；
- account/settings；
- Android release；
- mobile sync/offline。

## 3. Fix data-quality boundaries before visual polish

优先处理：
- URL/email/path 不能污染词汇；
- fallback 保留段落/section；
- DOM 真实空格；
- manual POS 不乱填；
- tokenizer failure 明确。

这些问题一旦写错数据，后续 UI 再漂亮也会放大错误。

## 4. Keep one owner for each formal learning mutation

外部审查重点：
- 谁创建 WordSense；
- 谁创建/修改 sense ReviewCard；
- 谁能写 ReviewLog；
- 谁能改变 FSRS；
- Finish Reading 的被动动作；
- mobile sync/operation ledger。

目标是一个行为只有一条正式写入路径。

## 5. Mobile sync before mobile feature expansion

移动端先证明：
- idempotency；
- offline queue；
- conflict；
- App restart recovery；
- duplicate rating protection；
- device revocation。

这些通过以后，再扩大移动端功能。

## 6. Product simplification

普通用户一级入口优先：
- Home；
- Reading；
- Review；
- Vocabulary；
- My/Settings。

Browser、Card Info、Custom Study、复杂统计、调度控制保留在高级入口，直到真实用户证明需要更高曝光。

## 7. Platform release gates

Android：
- current build；
- release artifact；
- signing；
- device；
- Play testing/policies。

iOS：
- macOS/Xcode；
- signing；
- simulator/device；
- TestFlight；
- App Store。

不允许跨平台推断完成。

## 8. Performance after measurement

先测：
- slow query；
- N+1；
- P95/P99；
- DB connections；
- tokenizer latency；
- lookup duplicate requests；
- sync queue backlog。

有数据后再决定：
- cache；
- queue tuning；
- DB split；
- CDN/object storage；
- horizontal scale。

不根据“以后可能有很多用户”提前建复杂架构。
