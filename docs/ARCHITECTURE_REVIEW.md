# Architecture Review — Initial Findings

这是第一轮问题地图，不等于最终重构计划。

## 1. 单一源码正本

Web/PC、Android、iOS 共享中央 Laravel 后端、账号、WordSense、ReviewCard、ReviewLog、FSRS、同步和备份语义。

社区经验没有给出“monorepo 永远更好”的统一答案，但反复出现的权衡是：共享契约和跨端改动频繁时，单仓可以降低多仓联动成本；代价是需要更清楚的 owner、构建边界和平台级测试。

参考：
- https://github.com/MobileNativeFoundation/discussions/discussions/31
- https://github.com/react-native-community/discussions-and-proposals/discussions/941

对 LinguaCafe：当前不建议按 Android/iOS/PC 复制三套源码仓；应在同仓里把平台构建和验收边界写清。

## 2. 当前主要风险簇

### 数据权威与副作用 owner
持续核查 Reader 中哪些动作只是展示、哪些创建 WordSense、哪些写 ReviewLog、哪些改变 FSRS，以及移动离线队列如何保证重复请求只生效一次。

### 大型编排组件
判断标准不是行数，而是是否拥有多个互相独立的数据真相、是否复制后端策略、是否难以做 focused tests、一个小需求是否反复触及大量无关模块。

### legacy 兼容
target_type=word、旧 stage、旧入口等存在历史兼容责任。任何退休必须先做依赖和数据审计。

### 移动 API / sync / offline
重点审查幂等、operation ledger、undo/redo、conflict、local queue、server authority、App 重启恢复。

### 发布和环境所有权
当前公开仓把本地环境配置、生成产物和正式源码混在 Git 跟踪范围内，说明“什么属于源码”的边界还需要收口。这是架构治理问题，不只是 .gitignore 小问题。

## 3. Private House / 字幕原则

- 一个真实需求对应一个最短正确路径。
- 现有 owner 能承担就不新建第二套。
- 不建立没有当前故障/需求支撑的 fallback。
- 高风险不变量用 harness/test 固定。
- 稳定的昂贵决定才写 ADR。
- 一次只收口一个能独立验收的责任切片。
