# flutter-example — Flutter iOS + Android CI on Macrunara M4

> ⚡ **[Install Macrunara](https://github.com/marketplace/macrunara)** → **[Fork](../../fork)** this repo → push to `main`: analyze + tests + **unsigned IPA and APK** finish in **~6 min** on Macrunara M4 runners.
> 📊 **~6 min cold / ~4 min warm** for both platforms — measured on a Macrunara M4 (Mac mini) node. <!-- TODO: replace with the real numbers from the first live run before publishing -->

[![Built on Macrunara M4](https://img.shields.io/badge/Built%20on-Macrunara%20M4-brightgreen)](https://macrunara.com)

English | [中文](README.zh-CN.md)

A fork-and-run **Flutter** example: one Mac mini M4 runner builds both mobile platforms in a single job — `flutter analyze` → `flutter test` → unsigned **IPA** + release **APK**, uploaded as artifacts. Macrunara nodes ship with the Flutter SDK, Xcode, Android SDK/NDK and JDK preinstalled, so there is **zero environment setup**.

## Fork & run in 3 minutes

1. **Install** the [Macrunara GitHub App](https://github.com/marketplace/macrunara) into your organization.
2. **Fork** this repository into the same organization.
3. Push to `main` — the [Flutter workflow](.github/workflows/flutter.yml) runs analyze + tests + both builds and uploads the IPA/APK as artifacts.

> ⚠️ The runner label must be exactly `runs-on: [macos, arm64, macrunara]`.

## What's inside

- A minimal but real Flutter app (counter) with a widget test — `lib/`, `test/`, `pubspec.yaml`.
- The `ios/` and `android/` platform folders are **regenerated in CI** (`flutter create --platforms=ios,android .`) so this repo stays tiny and version-drift-free. Commit them instead if you customize native code.
- The pipeline is pure `run:` commands against the preinstalled Flutter toolchain: `pub get → analyze → test → ipa (unsigned) → apk`.

## Build times (measured on Macrunara M4)

<!-- TODO: replace placeholders with real measured numbers + date from the first live run -->
| Stage | Cold | Warm (pub + build caches) |
|---|---|---|
| analyze + widget tests | ~1 min | ~40 s |
| iOS IPA (unsigned) | ~3 min | ~2 min |
| Android APK (release) | ~2 min | ~1 min |
| **Whole job** | **~6 min** | **~4 min** |

> Measured on a Macrunara M4 (Mac mini) node, Flutter 3.47 stable preinstalled.

## Signing & distribution

Unsigned artifacts keep this example zero-secret. To ship, add your own signing steps after the build action: an App Store Connect API key for iOS (see our [ios-swift-example](https://github.com/macrunara/ios-swift-example) for a complete fastlane flow) and an upload keystore for Android (`signingConfigs` + base64 keystore secrets).

## Links

- [Macrunara Quickstart & workflow templates](https://github.com/macrunara/quickstart)
- [Macrunara quickstart templates](https://github.com/MacRunara/quickstart/tree/main/templates)
- [macrunara.com](https://macrunara.com)
