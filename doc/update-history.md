# libmpv-darwin-build 修改历史（Git 完整复现）

> 锚点：`main df6799f`（2026-10-21）｜全仓 **210** 条；相对 `upstream/main` 本地分叉 **3** 条
> 五件套：[workflow-diagram.md](./workflow-diagram.md)｜[architecture.md](./architecture.md)｜[backlog.md](./backlog.md)｜[test-suite.md](./test-suite.md)
> 消费方：[media-kit](../../media-kit/doc/update-history.md)

> 关键口径：HLS/SPM/iOS 音频会话等来自上游；**本地分叉只有 Lua 与 AF 滤镜 3 条**。

## 1. 复现命令

```bash
git log --date=short --pretty=format:'%h %ad %an %s'
git log --date=short --pretty=format:'%h %ad %an %s' upstream/main..HEAD
git log --author=gaoxing64 --date=short --pretty=format:'%h %ad %s'
```

## 2. 本地分叉（相对 upstream/main）

| 日期 | 提交 | 作者 | 内容 |
| --- | --- | --- | --- |
| 2026-09-28 | `df6799f` | G | fix(lua): ar/ranlib 改用 Xcode 工具链绝对路径 |
| 2026-09-28 | `453562a` | G | fix(lua): meson compile 需显式指定 external_project 目标名 |
| 2026-09-28 | `49443a3` | G | feat(lua): 补回 Lua 支持并启用音量标准化所需 AF 滤镜 |

## 3. fork 作者提交（3 条）

| 日期 | 提交 | 作者 | 内容 |
| --- | --- | --- | --- |
| 2026-09-28 | `df6799f` | G | fix(lua): ar/ranlib 改用 Xcode 工具链绝对路径 |
| 2026-09-28 | `453562a` | G | fix(lua): meson compile 需显式指定 external_project 目标名 |
| 2026-09-28 | `49443a3` | G | feat(lua): 补回 Lua 支持并启用音量标准化所需 AF 滤镜 |

## 4. 全量时间线（210 条，新→旧）

| 日期 | 提交 | 作者 | 内容 |
| --- | --- | --- | --- |
| 2026-09-28 | `df6799f` | G | fix(lua): ar/ranlib 改用 Xcode 工具链绝对路径 |
| 2026-09-28 | `453562a` | G | fix(lua): meson compile 需显式指定 external_project 目标名 |
| 2026-09-28 | `49443a3` | G | feat(lua): 补回 Lua 支持并启用音量标准化所需 AF 滤镜 |
| 2026-08-11 | `93008b7` | P | fix(ffmpeg): improve HLS probing for disguised streams |
| 2026-05-23 | `a6e3dd6` | 0chencc | feat(spm): emit per-framework zip artifacts for xcframeworks builds (#4) |
| 2026-03-25 | `89406df` | 0x535A | fix: Delete AVAudioSessionCategoryOptionMixWithOthers to enable Media Controller on iOS (#3) |
| 2025-12-10 | `3b97d45` | P | ci: upload release |
| 2025-12-10 | `af4346e` | 林晨 | feat: ad blocker (#2) |
| 2025-12-10 | `f6e9053` | P | fix: fix build (#1) |
| 2025-12-09 | `e27075b` | P | Revert "fix int-to-pointer warning" |
| 2025-12-09 | `7313b7a` | P | fix int-to-pointer warning |
| 2025-12-09 | `a03380b` | P | ci: bump upload actions |
| 2025-12-09 | `4e7b3b9` | P | ci: bump macos runner |
| 2025-12-09 | `d30355c` | P | chore: add workflow dispatch |
| 2024-11-01 | `9ecf133` | P | update build.sh |
| 2024-11-01 | `84a706c` | P | backport fvp hls patch to ffmpeg |
| 2024-10-15 | `ad03c27` | Hitesh Kumar S | Merge pull request #32 from media-kit/feat/image-support |
| 2024-10-14 | `1b3f57b` | Hitesh Kumar S | feat: enable some image encoders/decoders |
| 2024-10-14 | `8d4bbea` | Hitesh Kumar S | Merge pull request #31 from 23doors/fix-uchardet |
| 2024-08-30 | `64ad4fd` | Robert Kopacze | fix: uchardet build |
| 2023-11-22 | `ca4e7f9` | Callum Moffat | Merge pull request #26 from moffatman/simlink |
| 2023-11-22 | `5b38a99` | birros | fix(ffmpeg): fix pkg-config binary search |
| 2023-11-22 | `e814f4f` | birros | Revert "Add pkg-config in runner" |
| 2023-11-21 | `d279d0d` | Callum Moffat | Add pkg-config in runner |
| 2023-11-21 | `08646fd` | Callum Moffat | Fix compilation in Xcode 15 |
| 2023-11-14 | `18cd32f` | Hitesh Kumar S | feat(mpv): mix with others |
| 2023-09-24 | `4286f55` | Julien Muret | Merge pull request #23 from moffatman/main |
| 2023-09-16 | `5896a83` | birros | Revert "refactor: rename encodersgpl flavor to encoders" |
| 2023-09-16 | `0b780c5` | birros | fix(cmake): fix sysroot collision |
| 2023-09-16 | `0995f3c` | birros | fix(cmake): fix sys_root arch |
| 2023-09-16 | `8831261` | birros | fix(cmake): add sys_root property |
| 2023-09-16 | `c88cfcb` | birros | docs(uchardet): add todo about double build |
| 2023-09-16 | `190cb01` | birros | refactor(mbedtls): use meson.build |
| 2023-09-16 | `f5efd08` | birros | refactor: rename encodersgpl flavor to encoders |
| 2023-09-16 | `ce8eaf6` | birros | ci: add encodersgpl flavor builds |
| 2023-09-16 | `965054d` | birros | refactor(make): change dependencies order |
| 2023-09-16 | `eb1eec0` | birros | docs: improve dependencies graph |
| 2023-09-16 | `2dee776` | birros | feat(tool-versions): add nasm and python3 |
| 2023-09-16 | `0906626` | birros | feat: remove `update-downloads-lock` |
| 2023-09-16 | `9f6e99c` | Callum Moffat | Install nasm in CI |
| 2023-09-15 | `2e6c6be` | Callum Moffat | encodersgpl flavor |
| 2023-09-15 | `1a0757c` | Julien Muret | Merge pull request #22 from birros/fix/macos-silicon |
| 2023-09-15 | `461ee49` | birros | ci: fix missing go |
| 2023-09-15 | `1001ccb` | birros | ci: bump to macos-13 |
| 2023-09-15 | `32fe10e` | birros | fix(make): fix macOS Silicon arch |
| 2023-09-03 | `b396470` | Julien Muret | Merge pull request #20 from birros/fix/dts |
| 2023-09-03 | `e89d635` | birros | fix(ffmpeg): fix dts support |
| 2023-08-30 | `77caf9c` | Julien Muret | Merge pull request #19 from birros/feat/av1 |
| 2023-08-30 | `474275d` | birros | feat: add dav1d support |
| 2023-08-30 | `10e6f92` | birros | build: bump tools & deps versions |
| 2023-08-26 | `2dfe071` | Julien Muret | Merge pull request #17 from media-kit/alexmercerind-patch-1 |
| 2023-08-25 | `1f830ca` | Hitesh Kumar S | fix: --enable-decoder=movtext |
| 2023-08-24 | `189810a` | Julien Muret | Merge pull request #13 from media-kit/fix/vp9-hwaccel |
| 2023-08-24 | `e52d7f2` | Julien Muret | Merge branch 'main' into fix/vp9-hwaccel |
| 2023-08-24 | `850ed6a` | Julien Muret | Merge pull request #15 from 23doors/fix/hls-mp4-seek |
| 2023-08-24 | `6409edc` | Julien Muret | Merge pull request #16 from 23doors/fix/image-based-subs |
| 2023-08-23 | `ee400cf` | birros | build(mpv): mv zlib option to common video options |
| 2023-08-23 | `1a0593b` | birros | fix(ffmpeg): fix vp9 patch |
| 2023-08-23 | `eb4f310` | Robert Kopacze | fix: image based subtitles |
| 2023-08-23 | `7fb561e` | Robert Kopacze | fix: HLS MP4 seek |
| 2023-08-23 | `aa1168e` | Hitesh Kumar S | fix: VP9 HWAccel https://trac.ffmpeg.org/ticket/9599 |
| 2023-08-23 | `0302ff7` | Hitesh Kumar S | fix(ios): H/W acceleration w/ AV_PIX_FMT_BGRA |
| 2023-08-23 | `53ab7b1` | Julien Muret | Merge pull request #12 from media-kit/mov_text |
| 2023-08-23 | `2438e9f` | Hitesh Kumar S | fix: --enable-decoder=mov_text |
| 2023-08-11 | `589527d` | birros | build(ffmpeg): fix dash base url escaping |
| 2023-08-08 | `67d5388` | birros | build(ffmpeg): add `--enable-protocol=crypto` |
| 2023-08-04 | `95778ac` | birros | build: add arch libs to the output |
| 2023-08-04 | `2513893` | Julien Muret | Merge pull request #10 from birros/feat/add-config-flavor |
| 2023-08-04 | `23ef453` | birros | build(mpv): remove flavor for mpv build |
| 2023-08-03 | `597ba7a` | birros | fix(frameworks): add short version metadata |
| 2023-08-03 | `570a279` | birros | build(ffmpeg): fix missing video-default hwaccels |
| 2023-08-01 | `7b90de8` | birros | build(ffmpeg): fix audio-full crash w/ `media_kit` |
| 2023-08-01 | `310a711` | birros | docs(README): update project layout |
| 2023-07-31 | `e468ef7` | birros | build(mpv): create DISABLE_ALL_OPTIONS as ffmpeg |
| 2023-07-31 | `905f751` | birros | build: add debug.zip |
| 2023-07-31 | `d295cf1` | birros | docs(Makefile): add docs about syntax used |
| 2023-07-31 | `66c5cb8` | birros | docs(README): reorder sections |
| 2023-07-31 | `89c36f3` | birros | docs(ffmpeg): remove TODO |
| 2023-07-31 | `c98eed0` | birros | build(scripts): cleanup scripts layout and naming |
| 2023-07-30 | `cd25d8c` | birros | build(mpv): fix macOS audio startup crash |
| 2023-07-29 | `ccb1998` | birros | build(ffmpeg): add flavor (default / full) |
| 2023-07-28 | `0aad673` | birros | docs: add missing libxml2 commercial use |
| 2023-07-27 | `9a17afc` | birros | build(make): change PATH order |
| 2023-07-27 | `488bf69` | birros | build: add libxml2 |
| 2023-07-25 | `7677fa2` | birros | docs: update Notes section |
| 2023-07-25 | `33ce301` | birros | build: bump dependencies |
| 2023-07-25 | `e327713` | birros | ci: fix missing tool-versions.lock |
| 2023-07-25 | `f2fc951` | birros | build: remove Taskfile & some updates |
| 2023-07-25 | `854cf29` | birros | build: Makefile first iteration |
| 2023-07-17 | `9fb14ad` | Julien Muret | Merge pull request #9 from birros/feat/lower-min-versions |
| 2023-07-16 | `967b956` | birros | build(iossimulator): fix min version to 12.0 |
| 2023-07-16 | `bce6330` | birros | build(ios): bump min iOS version 13.0 -> 9.0 |
| 2023-04-26 | `e4b355c` | Julien Muret | Merge pull request #7 from birros/fix/lowest-macos-version |
| 2023-04-26 | `0432556` | birros | docs: move CI comment |
| 2023-04-26 | `cf2cfa1` | birros | Revert "ci: remove flat build" |
| 2023-04-26 | `636bb7d` | birros | ci: remove flat build |
| 2023-04-26 | `c5e4b0e` | birros | build: bump min macOS version 10.8 -> 10.9 |
| 2023-04-26 | `4c538d2` | birros | doc: add note about CI limit |
| 2023-04-26 | `1f0eb7c` | birros | Revert "ci: add build-flat rule" |
| 2023-04-26 | `d10e570` | birros | fix(frameworks): fix MIN_OS_VERSION logic |
| 2023-04-25 | `6743fc4` | birros | feat(tool-versions): add macos version |
| 2023-04-25 | `746728b` | birros | ci: add build-flat rule |
| 2023-04-25 | `5afa9c3` | birros | ci: try flat build |
| 2023-04-25 | `77e5ea4` | birros | ci: debug ios video build |
| 2023-04-25 | `a51eb5a` | birros | ci: debug macos video build |
| 2023-04-25 | `b96d971` | birros | fix(lock): use openbsd cdn |
| 2023-04-25 | `ef5bbfb` | birros | ci: macos-latest -> macos-12 |
| 2023-04-25 | `e0b762c` | birros | build: bump min macOS versioin 11.0 -> 10.8 |
| 2023-04-14 | `35399b7` | Julien Muret | Merge pull request #6 from birros/feat/audio-libs |
| 2023-04-14 | `4c5f221` | birros | docs: add notes about min versions and libass |
| 2023-04-14 | `389090b` | birros | build: update mpv-remove-libass.patch |
| 2023-04-14 | `c8f2561` | birros | build: fix mpv-remove-libass.patch |
| 2023-04-13 | `1a07d74` | birros | ci: improve version determination |
| 2023-04-13 | `e2f0a7d` | birros | build: add audio variant |
| 2023-04-11 | `47943e4` | birros | build: rename packages -> archives |
| 2023-04-11 | `e2a3b7d` | birros | buid: move tasks to shell scripts |
| 2023-04-05 | `d5cc06b` | Julien Muret | Merge pull request #5 from birros/fix/macos-xcframewoks |
| 2023-04-05 | `b507c62` | birros | build(packages): fix broken symlinks when copying |
| 2023-04-05 | `56a8282` | birros | build: fix macOS `.framework` layout |
| 2023-04-03 | `9f10798` | Julien Muret | Merge pull request #4 from birros/refactor/update-identifier-2 |
| 2023-04-03 | `532c3c0` | birros | build: update identifier #2 |
| 2023-04-03 | `9ab6fed` | Julien Muret | Merge pull request #3 from birros/refactor/update-identifier |
| 2023-04-03 | `401f652` | birros | build: update identifier |
| 2023-04-03 | `b8c690c` | birros | docs: update usage |
| 2023-04-03 | `8cb3d35` | Julien Muret | Merge pull request #2 from birros/feat/add-xcframework |
| 2023-04-03 | `92d0215` | birros | build(ios): fix xcframeworks-ios-universal deps |
| 2023-04-02 | `a40e289` | birros | build: add packages for xcframeworks |
| 2023-04-02 | `8da1876` | birros | build: add xcframeworks |
| 2023-04-02 | `8813597` | birros | build: add frameworks |
| 2023-04-02 | `14505bb` | birros | build(macos): up min version of macOS to 11.0 |
| 2023-04-02 | `776cf5a` | birros | build(iossimulator): fix ios simulator arm64 build |
| 2023-04-02 | `2bc92aa` | birros | build(packages): remove VERSION check |
| 2023-04-02 | `13c9ef5` | birros | build(tool-versions): add xcode |
| 2023-04-02 | `2d8c9bc` | birros | build: add default to VERSION var |
| 2023-03-30 | `7da641e` | Julien Muret | Merge pull request #1 from birros/fix/darwin-libs |
| 2023-03-30 | `dbe9bdd` | birros | build(ios): add ios simulator build |
| 2023-03-30 | `d4a59ef` | birros | build: fix pkg-config os |
| 2023-03-30 | `2c1bd38` | birros | build(macos): rename darwin to macos |
| 2023-03-20 | `91d4fa3` | birros | fix(ios): fix HDR playback on iOS |
| 2023-03-19 | `8b074d5` | birros | build: add ios support |
| 2023-03-12 | `671c80b` | birros | build: rename some golang commands |
| 2023-03-12 | `6003387` | birros | build: replace release-note by tool-versions.lock |
| 2023-03-12 | `09f13c6` | birros | ci: clean pipeline |
| 2023-03-12 | `cb2768c` | birros | build(extract): redirect stderr to stdout |
| 2023-03-12 | `b0b8ca2` | birros | ci: try to fix build freezing #8 |
| 2023-03-12 | `0a09978` | birros | ci: try to fix build freezing #7 |
| 2023-03-12 | `86bb0ba` | birros | ci: try to fix build freezing #6 |
| 2023-03-12 | `2ecdc9c` | birros | ci: try to fix build freezing #5 |
| 2023-03-12 | `10146f1` | birros | ci: try to fix build freezing #4 |
| 2023-03-12 | `302c9eb` | birros | ci: try to fix build freezing #3 |
| 2023-03-12 | `6278944` | birros | ci: add preloading of go modules |
| 2023-03-12 | `ad1baa5` | birros | ci: fix setup go |
| 2023-03-12 | `2e329b0` | birros | ci: add setup go with cache |
| 2023-03-12 | `6168689` | birros | ci: try to fix build freezing #2 |
| 2023-03-12 | `ad58793` | birros | ci: try to fix build freezing |
| 2023-03-12 | `7a2668f` | birros | ci: test libressl build |
| 2023-03-12 | `75f7203` | birros | build: fix release-note |
| 2023-03-12 | `d6956db` | birros | ci: add upload & release |
| 2023-03-12 | `c39ea44` | birros | build: fix golang errors |
| 2023-03-12 | `62ba62f` | birros | build: update golang version in .tool-versions |
| 2023-03-12 | `e5cbb43` | birros | build: downgrade to go 1.17 |
| 2023-03-12 | `cb20139` | birros | ci: add print tool versions |
| 2023-03-12 | `49d5c02` | birros | ci: Initial setup |
| 2023-03-12 | `126c2ba` | birros | build: rename repo |
| 2023-03-12 | `b2414cb` | Julien Muret | feat: add LICENSE |
| 2023-03-12 | `eeee7a4` | birros | build: up tool-versions rule & add release-note |
| 2023-03-12 | `e239fa1` | birros | build: rename tools-version rule |
| 2023-03-12 | `036f744` | birros | doc: add version to usage |
| 2023-03-12 | `f7aedd6` | birros | build: add packages |
| 2023-03-11 | `6874aa8` | birros | build(libressl): fix file permissions |
| 2023-03-11 | `642dd41` | birros | build: refactor Taskfile |
| 2023-03-11 | `138bae8` | birros | doc: move notes |
| 2023-03-11 | `1aee15e` | birros | doc: fix typo |
| 2023-03-11 | `fe56160` | birros | doc: add project layout |
| 2023-03-11 | `6088171` | birros | doc: update README.md |
| 2023-03-11 | `27734b8` | birros | build: remove sources folder |
| 2023-03-10 | `c9f2401` | birros | build: improve build flags |
| 2023-03-10 | `a587b3f` | birros | doc: add dependency graph |
| 2023-03-10 | `d8a72ed` | birros | build: add uchardet |
| 2023-03-10 | `a8d628e` | birros | build: update commercial use |
| 2023-03-10 | `c9c62c2` | birros | build: lock -> update & improve code |
| 2023-03-10 | `f140e10` | birros | refactor(download): improve code |
| 2023-03-10 | `bd15126` | birros | doc: update Todo |
| 2023-03-10 | `1f73219` | birros | build: add libressl |
| 2023-03-09 | `51ffe0d` | birros | build: use meson for pkg-config build |
| 2023-03-09 | `6159b15` | birros | build: update tool-versions |
| 2023-03-09 | `5a8cef6` | birros | build: improve meson support for ffmpeg |
| 2023-03-08 | `5675812` | birros | doc: update todo & resources |
| 2023-03-08 | `bf4abc4` | birros | build: add package fix, TERM & UNSETENV |
| 2023-03-08 | `c3fd776` | birros | doc: update README.md |
| 2023-03-08 | `7c85b7e` | birros | build: add macos version min |
| 2023-03-08 | `646b630` | birros | build: fix verbosity of external_project |
| 2023-03-07 | `34e418c` | birros | doc: update Todo |
| 2023-03-06 | `cb0f39a` | birros | build: add darwin/arm64 & universal build |
| 2023-03-06 | `3a96530` | birros | build: add cross-file for amd64 |
| 2023-03-06 | `0a04067` | birros | build: Makefile -> Taskfile |
| 2023-03-04 | `655dae8` | birros | build(ffmpeg): disable static |
| 2023-03-04 | `d16838e` | birros | build(ffmpeg): disable x11 |
| 2023-03-04 | `370d73c` | birros | build(ffmpeg): enable https |
| 2023-03-04 | `b255d11` | birros | build(ffmpeg): add videotoolbox |
| 2023-03-04 | `7fc626f` | birros | build(ffmpeg): disable avdevice & postproc |
| 2023-03-04 | `44aa77e` | birros | build(harfbuzz): add conf |
| 2023-03-04 | `9af7721` | birros | build(pkg-config): add conf |
| 2023-03-04 | `6b1a667` | birros | build(fribidi): add config |
| 2023-03-04 | `3d4345c` | birros | build(libass): add conf |
| 2023-03-04 | `38dd3fa` | birros | feat: enable CoreAudio |
| 2023-03-03 | `2a46b24` | birros | doc: add resources |
| 2023-03-03 | `2d268c4` | birros | build: add minimal macOS x64 build |
| 2023-03-02 | `aa0a3c0` | birros | doc: add minimal linux workflow |
| 2023-03-02 | `15d40b7` | birros | first commit |

## 5. 当前状态

- 分支 `main`，HEAD `df6799f`；相对 `upstream/main` 领先 3 条（Lua 2 条 + AF 滤镜 1 条）。
- HLS/SPM/iOS 音频会话等来自上游；其余为 2023 年 Nix 构建体系与上游维护。
