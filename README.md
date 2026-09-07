# LinguaCafe Architecture Review

LinguaCafe 的公开架构、技术债、UI/UX、测试与三端成熟度审查仓。

源码正本：
- https://github.com/gufyhvvyfycyddy-code/LinguaCafe-local
- 当前冻结审查基线：`6989ed27c933716f9069bb9b14fba92624081fc4`
- 当前源码 `master` 还包含冻结基线之后的安全、依赖与发布修复，当前审查状态同步至源码合并提交 `2abc82df754525c19733382200aaf72a930d436a`；这些后续提交不自动继承冻结基线的浏览器验收结论。

产品上线与运营审查：
- https://github.com/gufyhvvyfycyddy-code/LinguaCafe-product-launch

## 从这里开始

1. [FINAL_REVIEW_HANDOFF.md](FINAL_REVIEW_HANDOFF.md) — 外部审查总入口
2. [REVIEW_START_HERE.md](REVIEW_START_HERE.md)
3. [CURRENT_STATUS.md](CURRENT_STATUS.md)
4. [DEPENDENCY_HIGH_RISK_DISPOSITION_2026-09-07.md](DEPENDENCY_HIGH_RISK_DISPOSITION_2026-09-07.md) — 当前剩余 High 的可达性与升级边界
5. [docs/PLATFORM_STATUS.md](docs/PLATFORM_STATUS.md)
4. [docs/ARCHITECTURE_REVIEW.md](docs/ARCHITECTURE_REVIEW.md)
5. [docs/PUBLIC_SECURITY_FINDINGS.md](docs/PUBLIC_SECURITY_FINDINGS.md)
6. [docs/COMMUNITY_RESEARCH.md](docs/COMMUNITY_RESEARCH.md)

## 审查原则

- 以源码、测试、真实运行证据为主，不以旧报告代替当前事实。
- 一个行为尽量只有一条主路径和一个事实 owner。
- 文件大本身不是重构理由；只有责任混乱、重复事实、难以测试或真实缺陷才进入架构问题。
- 稳定决定进入 ADR；可执行问题进入 Issue；探索材料留在 docs。
- Web/PC、Android、iOS 共用同一后端和领域模型，所以保留单一源码正本，避免复制三套“最新代码”。

## 主要审查问题

- 当前最危险的架构问题是什么？
- 哪些问题是真实产品阻塞，哪些只是代码洁癖？
- Reader / Sense Review / FSRS / ReviewLog / Sync / Offline 的 owner 是否清楚？
- 三端共享 API 和领域模型是否适合继续扩展？
- 当前安全、隐私、备份和发布工程是否足以支持真实用户？
- Web/PC 当前已完成的真实浏览器链路与仍未验证的后台/破坏性路径之间，边界是否足够清楚？
- 哪些历史兼容路径应该保留，哪些可以退休？
