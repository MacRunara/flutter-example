# flutter-example — Flutter 双端 CI(Macrunara M4)

> ⚡ **[安装 Macrunara](https://github.com/marketplace/macrunara)** → **Fork** 本仓库 → 推送 `main`:analyze + 测试 + **未签名 IPA 和 APK** 全部在 **约 6 分钟**内完成。
> 📊 双端合计 **冷构建约 6 分钟 / 有缓存约 4 分钟**,实测于 Macrunara M4(Mac mini)节点。<!-- TODO:发布前用首次真实运行数据替换 -->

[![Built on Macrunara M4](https://img.shields.io/badge/Built%20on-Macrunara%20M4-brightgreen)](https://macrunara.com)

[English](README.md) | 中文

一个可直接 fork 运行的 **Flutter** 示例:一台 Mac mini M4 runner 在一个 job 里构建双端 —— `flutter analyze` → `flutter test` → 未签名 **IPA** + release **APK**,产物自动上传。节点预装 Flutter SDK、Xcode、Android SDK/NDK、JDK,**零环境配置**。

## 三步跑起来

1. 组织内[安装 Macrunara App](https://github.com/marketplace/macrunara);
2. Fork 本仓库;
3. 推送 `main` —— [flutter.yml](.github/workflows/flutter.yml) 自动跑完整流水线并上传 IPA/APK。

> ⚠️ runner 标签必须严格写成 `runs-on: [macos, arm64, macrunara]`。

## 说明

- 最小但完整的 Flutter 计数器应用 + widget 测试(`lib/`、`test/`、`pubspec.yaml`);
- `ios/`、`android/` 平台目录在 CI 里用 `flutter create --platforms=ios,android .` 现场生成,保持仓库精简;如需定制原生代码,把这两个目录提交进仓库即可;
- 流水线为纯 `run:` 命令,直接使用节点预装的 Flutter 工具链:`pub get → analyze → test → ipa(未签名)→ apk`。

## 构建时长(实测) <!-- TODO:发布前替换为真实数据 -->

| 阶段 | 冷构建 | 有缓存 |
|---|---|---|
| analyze + widget 测试 | ~1 分钟 | ~40 秒 |
| iOS IPA(未签名) | ~3 分钟 | ~2 分钟 |
| Android APK(release) | ~2 分钟 | ~1 分钟 |
| **整个 job** | **~6 分钟** | **~4 分钟** |

## 签名与分发

本示例保持零 secret（不签名）。需要上架时参考：[ios-swift-example](https://github.com/macrunara/ios-swift-example) 的 fastlane + App Store Connect API Key 完整流程；Android 侧配置 `signingConfigs` + base64 keystore secrets。

## 链接

- [Macrunara Quickstart 与模板库](https://github.com/macrunara/quickstart)
- [Macrunara quickstart 模板](https://github.com/MacRunara/quickstart/tree/main/templates)
- [macrunara.com](https://macrunara.com)
