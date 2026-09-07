# Public Security Findings

## P0 — 公开源码卫生门禁失败

### 现象

只读 Git tree 核查确认，源码仓当前公开历史/当前树包含：
- 应由本地环境管理、而不应作为公开源码真相的环境配置；
- 历史浏览器自动化 console/page 产物；
- 其他需要继续逐文件确认的生成与本地测试产物。

本文件故意不复制任何可能的 secret、token、cookie、password 或 session 内容。

### 用户影响

如果环境配置中曾经存在真实凭据，公开仓会造成凭据泄漏风险；即使当前值已经失效，公开历史也会误导后续开发者继续提交本地配置。

### 当前证据

- git ls-files / git ls-tree origin/master 只读核查。
- GitHub 仓当前为 Public。
- 2026-09-07 启用 GitHub Secret Scanning + Push Protection。
- 启用后 GitHub API 当前报告 0 个 secret-scanning alerts。

### 为什么 0 alerts 仍不能关闭问题

Secret Scanning 依赖 GitHub 支持的 pattern/validation；真实敏感数据如果不匹配支持模式，仍可能不会产生 alert。

### 正确处理顺序

1. 不读取/复制 secret 到 Issue 或审查文档。
2. 由凭据所有者确认是否存在仍有效 secret。
3. 如果曾暴露真实 secret，先 revoke/rotate。
4. 再决定是否需要 Git history sensitive-data removal。
5. 当前分支移除本地环境文件的 Git 跟踪，并提供安全 example/template。
6. 删除或隔离浏览器历史产物。
7. 重新扫描当前 tree 和历史。
8. 重新确认所有公开仓 Push Protection 仍开启。

### 官方参考

- https://docs.github.com/en/code-security/concepts/secret-security/secret-scanning
- https://docs.github.com/en/code-security/concepts/secret-security/push-protection
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository
