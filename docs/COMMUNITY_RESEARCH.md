# Community Research Log

社区经验只作为参考，不覆盖源码事实和产品决定。

## Monorepo

### Mobile Native Foundation
讨论指出 monorepo 可以共享 iOS/Android 工具、测试和底层模块，但大型 monorepo 需要明确 owner、构建边界和维护投入。
https://github.com/MobileNativeFoundation/discussions/discussions/31

### React Native community
2025 的讨论仍围绕 Web + mobile monorepo 的共享代码、Vite/Metro 工具边界展开，说明“共享代码”不等于“共享全部运行时”。
https://github.com/react-native-community/discussions-and-proposals/discussions/941

### Turborepo community
2026 的讨论常见模式仍是：一个后端、多个客户端、共享 API contract；Web 和 mobile 有独立 build/release pipeline。
https://github.com/vercel/turborepo/discussions/12957

## Public-repo security

GitHub 官方建议 public repo 使用 Secret Scanning、Push Protection、Code Scanning；已暴露真实 secret 时优先 revoke/rotate。
https://docs.github.com/en/code-security/concepts/secret-security/secret-scanning
https://docs.github.com/en/code-security/concepts/secret-security/push-protection
https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository
