# libmpv-darwin-build 工作流程图

> 锚点：`main df6799f`（2026-10-21）｜范围：Nix 构建链、产物矩阵、CI 发布、media-kit 消费
> 五件套：[architecture.md](./architecture.md)｜[update-history.md](./update-history.md)｜[backlog.md](./backlog.md)｜[test-suite.md](./test-suite.md)
> 消费方：[media-kit](../..//media-kit/doc/architecture.md)｜同族：[win32](../../libmpv-win32-video-cmake/doc/architecture.md)｜[android](../../libmpv-android-video-build/doc/architecture.md)

## 1. 一次构建的主链

```
CI 触发（tag / PR / workflow_dispatch）
  → checkout
  → 安装 Nix（DeterminateSystems，sandbox=true）
  → 把 Xcode_16.1.0.app 复制进 /nix/store 并手工登记 ValidPaths
  → nix build -v
       ├─ 读 packages.lock.nix（版本+SHA256）
       ├─ 逐包交叉编译：mbedtls → ffmpeg → lua → uchardet/libass → mpv
       ├─ 按 targets 组合：variant(audio|video) × flavor(default|full|encodersgpl)
       └─ 打包：libs（.tar.gz）与 xcframeworks（.tar.gz/.zip）
  → upload-artifact（result/*.tar.gz|zip）
  → tag 时 softprops/action-gh-release 发布
```

证据：`.github/workflows/ci.yaml:20-83`、`flake.nix:1-38`、`nix/utils/flake/create-cross-packages.nix`。

## 2. 包依赖链

```
mbedtls ─┐
dav1d ───┤
libxml2 ─┼→ ffmpeg → mpv → libs / frameworks / xcframeworks
libvpx ──┤        ↗
libx264 ─┘   lua ─┘
             uchardet、libass（仅 video）
```

- ffmpeg 补丁在 `nix/packages/mk-pkg-ffmpeg/default.nix:36-52` 依次打 5 个 patch。
- mpv 固定打 `mpv-fix-missing-objc.patch`；audio 变体额外打 `mpv-remove-libass.patch`（`mk-pkg-mpv/default.nix:40-48`）。
- Lua 走 meson external_project 包裹上游 `configure`（`mk-pkg-lua/meson.build:5-14`）。

## 3. 产物组合

```
os:      macos | ios | iossimulator
arch:    amd64 | arm64 | universal
variant: audio ⊂ video
flavor:  default ⊂ full ⊂ encodersgpl
format:  libs | xcframeworks
```

命名：`libmpv-<format>_<version>_<os>-<arch>-<variant>-<flavor>.tar.gz`（`README.md` 命名约定；`nix/utils/name/output.nix`）。

## 4. 产物进入 App 的路径

```
GitHub Release（tag）
  → media-kit 的 libs/{macos,ios} 更新 hash/URL
  → media_kit 在运行时加载 libmpv
  → simple_live_app 播放
```

改动二进制后必须同步更新 media-kit 侧的下载锁；否则 App 仍用旧库（见 [media-kit backlog](../../media-kit/doc/backlog.md)）。

## 5. 失败与兜底

| 失败点 | 表现 | 兜底 |
| --- | --- | --- |
| Xcode 不在 Nix store | `xcodebuild` 找不到 SDK | CI 手工复制并登记 `/nix/store`（`ci.yaml:35-43`） |
| Lua 交叉编译 | `ar/ranlib` 指向宿主工具 | 用 Xcode 工具链绝对路径（`df6799f`） |
| meson external_project | 目标名解析失败 | `meson compile` 显式指定目标（`453562a`） |
| ffmpeg 补丁上下文漂移 | `patch` 失败 | 按上游源码刷新 patch（见 backlog） |
| 未打 tag | 只上传 artifact，不发 Release | 手动下载 artifact 验证 |

## 历史锚点

| 流程 | 关键提交 |
| --- | --- |
| 本地 Lua + AF 滤镜 | `49443a3`、`453562a`、`df6799f` |
| HLS 探测（上游） | `93008b7` |
| SPM 分包（上游） | `a6e3dd6` |
| iOS 媒体控制（上游） | `89406df` |
