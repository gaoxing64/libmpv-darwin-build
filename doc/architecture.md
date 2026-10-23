# libmpv-darwin-build 架构与选型对照

> 锚点：`main df6799f`（2026-10-21）｜范围：Nix flake、交叉构建、补丁、产物、CI
> 五件套：[workflow-diagram.md](./workflow-diagram.md)｜[update-history.md](./update-history.md)｜[backlog.md](./backlog.md)｜[test-suite.md](./test-suite.md)
> 消费方：[media-kit](../../media-kit/doc/architecture.md)｜同族：[win32](../../libmpv-win32-video-cmake/doc/architecture.md)｜[android](../../libmpv-android-video-build/doc/architecture.md)

## 1. 定位

macOS/iOS 的 libmpv 构建仓，产出 media-kit 直接消费的静态库/xcframework。上游是 `Predidit/libmpv-darwin-build`；HLS 探测、SPM 分包、iOS 音频会话均来自上游主线，**本 fork 相对 `upstream/main` 只领先 3 条：Lua 2 条 + AF 滤镜 1 条**。

## 2. 分层

| 层 | 位置 | 职责 |
| --- | --- | --- |
| 入口 | `flake.nix` | flakelight 定义 systems、overlay、devShell、perSystem packages |
| 交叉参数 | `cross-files/*.ini`、`nix/utils/cross-file` | 5 个 target 的 CC/SDK/sysroot |
| 包定义 | `nix/packages/mk-pkg-*` | 每个依赖一个 derivation + meson 包装 |
| 组合 | `nix/utils/{targets,constants}` | os/arch/variant/flavor 笛卡尔积 |
| 打包 | `nix/packages/mk-out-{libs,frameworks,archive,xcframeworks}` | 目录布局与压缩命名 |
| CI | `.github/workflows/ci.yaml` | macOS runner、Nix、Xcode、发布 |

依赖方向：`flake → packages → utils`，无反向引用。

## 3. 版本与工具链

| 项 | 值 | 证据 |
| --- | --- | --- |
| mpv | 0.36.0 | `packages.lock.nix:82-86` |
| ffmpeg | 6.0 | `packages.lock.nix:8-12` |
| Lua | 5.2.4 | `packages.lock.nix` lua 条目 |
| Xcode | 16.1.0 | `.github/workflows/ci.yaml:35-36` |
| macOS runner | macos-15 | `ci.yaml:22` |
| Nix systems | aarch64-darwin / x86_64-darwin | `flake.nix:20-23` |

## 4. 关键定制

> 来源：Lua 与 AF 滤镜为本地分叉（3 条）；HLS/SPM/iOS 媒体控制来自上游。

| 定制 | 原因 | 位置 |
| --- | --- | --- |
| `dynaudnorm/loudnorm/aresample/alimiter/acompressor` | 音量均衡；缺 `aresample` 会让 `loudnorm` 建图失败并静默失效 | `nix/packages/mk-pkg-ffmpeg/meson.build:169-175` |
| Lua 5.2.4 静态链入 | 恢复 mpv 内置脚本（stats/osc 等） | `nix/packages/mk-pkg-lua/`、`mk-pkg-mpv/default.nix` |
| HLS kazumi 合并补丁 + fdash base-url | 伪装 HLS 流的探测/seek | `patches/ffmpeg-hls-kazumi-combined.patch`、`ffmpeg-fix-dash-base-url-escape.patch` |
| iOS HDR texture / VP9 hwaccel | iOS 渲染与硬解 | `patches/ffmpeg-fix-ios-hdr-texture.patch`、`ffmpeg-fix-vp9-hwaccel.patch` |
| 删除 AVAudioSession mixWithOthers | 让 iOS 媒体控制可用 | `89406df` |
| SPM per-framework zip | Swift Package 分发 | `a6e3dd6` |

## 5. 产物矩阵

`libs`/`xcframeworks` × `macos|ios|iossimulator` × `amd64|arm64|universal` × `audio|video` × `default|full|encodersgpl`。包含关系：`audio ⊂ video`、`default ⊂ full ⊂ encodersgpl`（`README.md`）。

## 6. 取舍与风险

- **选 Nix 而非手写脚本**：依赖可锁定、可复现；代价是 Xcode 必须塞进 `/nix/store`（`ci.yaml` 手工登记 hack）。
- **静态链 Lua**：避免运行时 dylib 查找；代价是每次 mpv 升级都要验证 external_project 目标名。
- **音频变体去 libass**：减小体积；代价是音频产物不能显示字幕。
- **风险**：上游 `Predidit` 补丁漂移；iOS 未在当前 Windows 开发机验证；Release 未做签名/公证；产物哈希需人工同步到 media-kit。

## 历史锚点

| 决策 | 提交 |
| --- | --- |
| Lua 5.2.4 + AF 滤镜 | `49443a3` |
| meson external_project 目标名 | `453562a` |
| ar/ranlib 用 Xcode 绝对路径 | `df6799f` |
