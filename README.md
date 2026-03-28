# Blunote Updates

Public update feed for the Blunote desktop app.

This repository stays public so desktop clients can fetch update manifests and
installer files without authentication.

## Files

- `latest-mac.json`: macOS update manifest
- `latest-win.json`: Windows update manifest
- platform installers referenced by the latest manifests

## Manifest compatibility contract

Older desktop clients are strict. To keep online updates backward compatible,
each manifest must follow these rules:

- UTF-8 without BOM
- plain JSON object only
- top-level keys must stay: `version`, `url`, `notes`
- no comments, no trailing commas, no extra wrapper fields
- keep URLs stable and absolute

Recommended format:

```json
{"version":"0.1.19","url":"https://cdn.jsdelivr.net/gh/xiaomaolu/blunote-updates@main/Blunote.Setup.0.1.19.exe","notes":"Release notes"}
```

## Manifest URLs

Preferred CDN endpoints:

- macOS: `https://cdn.jsdelivr.net/gh/xiaomaolu/blunote-updates@main/latest-mac.json`
- Windows: `https://cdn.jsdelivr.net/gh/xiaomaolu/blunote-updates@main/latest-win.json`

Raw GitHub also works as a fallback, but jsDelivr is the preferred public feed.

## Retention policy

This repository is a file host, so seeing both `0.1.15` and `0.1.16` is not a
logic bug by itself. Historical installers may remain for rollback/manual
recovery.

Going forward, keep it tidy:

- keep the latest stable installer for each platform
- keep one previous stable installer for rollback
- remove older superseded installers after a newer release is verified

Version numbers are global product versions, but platform packaging can skip a
version. For example, Windows currently keeps `0.1.19` and `0.1.16` because
`0.1.17` and `0.1.18` were not published as Windows update packages in this
repo, while macOS has its own separate latest package history.

## Release workflow

1. Build the desktop installer.
2. Upload the new installer files into this repo.
3. Update `latest-mac.json` or `latest-win.json`.
4. Verify the manifest bytes are BOM-free.
5. Commit and push.
