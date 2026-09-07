# Platform Status

| 平台 | 当前事实 | 仍缺的证据 | 当前判断 |
|---|---|---|---|
| Web / PC | Laravel + Vue 主产品；Reader、Sense Review、Browser、FSRS、AI Study Card 等已有大量实现与测试 | 最新远端与本地分叉后的统一基线；当前版本真实浏览器主流程回归 | Implemented / needs current acceptance |
| Android | mobile/android 工程存在；已有历史模拟器、有限离线、媒体等验收 | 当前 release build、AAB、签名、Play Console、真实设备/当前模拟器复验 | Implemented / store readiness unverified |
| iOS | mobile/ios Xcode 工程与发布材料存在 | macOS/Xcode build、签名、模拟器/真机、TestFlight、App Store Connect | Implementation present / external capability blocked |

## Android

Google Play 发布前必须重新核对当前 Data Safety、Privacy Policy、Account Deletion、测试轨和技术质量要求，不能沿用旧政策。

## iOS

仓库已有 App Store listing / privacy / reviewer flow 草案，但这些文档不等于 TestFlight/App Store 已完成。最终证据必须来自真实 macOS/Xcode/签名/设备/商店环境。
