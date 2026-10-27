# libmpv-darwin-build 测试案例库（面向 AI）

> 锚点：`main df6799f`（2026-10-21）｜本仓无单元测试，验收以构建产物为准
> 五件套：[workflow-diagram.md](./workflow-diagram.md)｜[architecture.md](./architecture.md)｜[update-history.md](./update-history.md)｜[backlog.md](./backlog.md)
> 消费方：[media-kit](../../media-kit/doc/architecture.md)

## 1. 怎么跑

```bash
# 本地（macOS + Nix + Xcode）
echo '"v0.0.1"' > nix/utils/default/version.nix
nix build -v
ls result/
# 单 target
nix build -v .#mk-out-archive-libs-macos-universal-video-default
```

CI：`.github/workflows/ci.yaml`，tag 触发发布。

## 2. 构建验收用例

| ID | 前置 | 步骤 | 期望 |
| --- | --- | --- | --- |
| TC-D-01 | Nix/Xcode 就绪 | `nix build -v` | 退出码 0；`result/` 出现全部 libs/xcframeworks tarball |
| TC-D-02 | 产物解包 | 检查 `libmpv-<format>_<ver>_<os>-<arch>-<variant>-<flavor>.tar.gz` | 命名符合 README 约定，数量与矩阵一致 |
| TC-D-03 | 解包 macos-universal-video-default | `lipo -info libmpv*.dylib` | 同时含 x86_64 与 arm64 |
| TC-D-04 | 解包 ios-universal | `lipo -info`/`vtool -show-build` | arm64 切片；最低系统版本符合 README |
| TC-D-05 | ffmpeg 产物 | `grep -E 'dynaudnorm|loudnorm|aresample|alimiter|acompressor' share/ffmpeg/configure.log` | 5 个滤镜均在 `--enable-filter` 列表 |
| TC-D-06 | libmpv 产物 | `sh scripts/verify_libmpv_artifacts.sh <libmpv.dylib> --config-source nix/packages/mk-pkg-ffmpeg/meson.build` | loudnorm 链与 h264/hevc/av1 解码器均 PASS；AV1 parser 查构建配方 |
| TC-D-07 | Lua/stats.lua | 同上，检查 `display-stats-toggle`、`display-page-1-toggle` | 均 PASS（mpv 0.36 缺分页开关，由 `patches/mpv-stats-page-toggle.patch` 补齐） |
| TC-D-08 | HLS 伪装流 | 播放一段伪装扩展名的 HLS | 能识别 demuxer 并起播（对照补丁 `hls-kazumi`） |
| TC-D-09 | iOS 媒体控制 | 真机播放，锁屏/控制中心操作 | 播放/暂停可用（对应 `89406df`） |
| TC-D-10 | audio 变体 | 解包 audio tarball | 无 libass；视频变体有 libass |

## 3. 发布前清单

1. `ci.yaml` 的 Xcode 路径/哈希与 runner 匹配。
2. tag 后 Release 附件齐全（`result/*.tar.gz|zip`）。
3. 记录产物 SHA256，更新 media-kit `libs/{macos,ios}` 的下载锁。
4. 在 macOS 跑一次 `nix build` 复现 CI 结果。

## 4. 已知限制

- 无法在 Windows 开发机执行；以上用例需 macOS runner 或真机。
- 没有自动化断言脚本；建议把 TC-D-05/06 写成 CI step（见 backlog P0-1）。

## 历史锚点

| 用例 | 守护的提交 |
| --- | --- |
| TC-D-05/06 滤镜 | `49443a3` |
| TC-D-09 iOS 媒体控制 | `89406df`（上游） |
