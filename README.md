# Blunote Updates / Blunote 更新仓库

Public update feed for Blunote installers and online update manifests.

Blunote 安装包下载与在线更新清单的公开仓库。

## Repository roles / 仓库定位

- Main app repository (planned open source): https://github.com/xiaomaolu/blunote
- iOS repository (private source): https://github.com/xiaomaolu/blunote-IOS
- Public update feed and installer links: https://github.com/xiaomaolu/blunote-updates

- 主应用仓库（计划开源）：https://github.com/xiaomaolu/blunote
- iOS 仓库（不开源）：https://github.com/xiaomaolu/blunote-IOS
- 公开更新仓库（仅安装包链接与在线更新）：https://github.com/xiaomaolu/blunote-updates

## What stays in this repo / 这个仓库保留什么

- `latest-win.json`: Windows update manifest / Windows 在线更新清单
- `latest-mac.json`: macOS update manifest / macOS 在线更新清单
- lightweight docs about update compatibility / 更新兼容性说明文档

Windows installers should be hosted as GitHub Release assets. macOS installers may be published either as Release assets or as Git LFS-backed direct-download files kept only for update distribution.

Windows 安装包应托管在 GitHub Releases 中。macOS 安装包可以使用 GitHub Releases，或仅为更新分发而保留为 Git LFS 直链文件。

## Manifest compatibility contract / 清单兼容约定

Older desktop clients are strict. To keep updates backward compatible:

旧版桌面客户端对清单格式较严格。为了保证兼容性：

- UTF-8 without BOM / 使用 UTF-8 且不要带 BOM
- plain JSON object only / 只能是纯 JSON 对象
- top-level keys must stay: `version`, `url`, `notes` / 顶层字段必须保持为 `version`、`url`、`notes`
- no comments, no trailing commas, no wrapper fields / 不要注释、不要尾逗号、不要额外包裹层
- keep URLs stable and absolute / URL 使用稳定的绝对地址

Recommended Windows format / 推荐的 Windows 格式：

```json
{"version":"0.1.23","url":"https://github.com/xiaomaolu/blunote-updates/releases/download/v0.1.23/Blunote.Setup.0.1.23.exe","notes":"EN: Sidebar tree cleanup, tag grouping, and sync improvements. | 中文：侧边栏树形结构优化、标签分组与同步体验改进。"}
```

## Public manifest URLs / 公共清单地址

Preferred CDN endpoints / 推荐 CDN 地址：

- macOS: `https://cdn.jsdelivr.net/gh/xiaomaolu/blunote-updates@main/latest-mac.json`
- Windows: `https://cdn.jsdelivr.net/gh/xiaomaolu/blunote-updates@main/latest-win.json`

Fallback raw endpoints / Raw 备用地址：

- macOS: `https://raw.githubusercontent.com/xiaomaolu/blunote-updates/main/latest-mac.json`
- Windows: `https://raw.githubusercontent.com/xiaomaolu/blunote-updates/main/latest-win.json`

## Release workflow / 发布流程

1. Build the desktop installer. / 构建桌面安装包。
2. Publish the installer to a stable direct-download URL. / 将安装包发布到稳定的直链地址。
3. Update `latest-win.json` or `latest-mac.json`. / 更新 `latest-win.json` 或 `latest-mac.json`。
4. Verify the manifest is BOM-free and backward compatible. / 确认清单无 BOM 且兼容旧客户端。
5. If macOS uses repo-hosted LFS files, update the tracked binaries and then push. / 如果 macOS 使用仓库内的 LFS 文件，还需要同步更新二进制并推送。

## Retention policy / 保留策略

- Keep manifests in the repo. / 仓库中保留清单文件。
- Keep Windows assets in GitHub Releases. / Windows 安装包保留在 GitHub Releases。
- macOS assets may live in GitHub Releases or as repo-hosted LFS files referenced by the manifest. / macOS 安装包可以放在 GitHub Releases，或作为清单引用的仓库内 LFS 文件。
- Remove superseded installers from the repo tree when replaced. / 仓库根目录中的旧安装包在替换后应移除。
- Historical releases remain downloadable from the Releases page. / 历史版本可继续从 Releases 页面下载。
