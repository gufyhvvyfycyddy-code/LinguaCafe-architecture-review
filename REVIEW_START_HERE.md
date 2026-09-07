# Review Start Here

## 产品一句话

LinguaCafe 让用户在真实英语材料中学习“这个词在这里是什么意思”，以 WordSense 作为学习内容，以 sense ReviewCard + FSRS 作为正式复习对象，并把原文来源保存为 WordSenseOccurrence。

## 当前技术结构

- Laravel 后端和中央数据库是最终权威。
- Web/PC 是最完整的管理和阅读界面。
- Android/iOS 是移动客户端，复用中央 API、有限离线包、操作队列和同步语义。
- 正式复习对象是 target_type=sense；target_type=word 只保留 legacy 兼容。
- AI 主要用于解释、翻译和消歧；默认不允许无确认地改变正式复习历史。

## 当前最先审查的事实

1. 源码仓公开安全门禁仍有 P0：当前公开源码树仍跟踪环境配置路径。精确敏感内容不在本仓公开复述，也未在本轮读取。
2. 早期本地/远端双向分叉已经通过非 force 方式完成历史收敛；当前远端源码 `master` 不再以该分叉作为阻塞项。
3. 历史 Playwright CLI 产物和 tokenizer Python bytecode 已从当前源码 `master` 清理。受保护的本地主工作区仍有未提交用户资产，因此仍不能整体 reset、clean 或 bulk push。
4. 冻结功能验收基线仍是 `6989ed27c933716f9069bb9b14fba92624081fc4`；当前源码 `master` 还包含之后的 PR #30/#31/#32/#34 修复与发布文档，这些后续提交需要按各自证据理解。
5. iOS 代码和发布材料存在，但缺 macOS/Xcode/签名/设备/TestFlight/App Store 的最终真实证据。
6. Android 有工程和历史模拟器证据，但最新 release/AAB/签名/Play Store 状态需要重新验证。

## 建议审查顺序

1. PUBLIC_SECURITY_FINDINGS
2. PLATFORM_STATUS
3. ARCHITECTURE_REVIEW
4. 源码仓 CURRENT_AI_CONTEXT / Documentation Index / ADR
5. Reader、Sense Review、Mobile API、Sync、Backup/Restore 的真实调用链
6. 当前 Issue 列表

## 请避免

- 不要把“文件很长”直接等同于“必须拆分”。
- 不要把历史验收报告当成当前运行证据。
- 不要建议复制三套源码仓。
- 不要建议绕过 testing DB、FSRS、ReviewLog、幂等或用户隔离门禁。
