# Blunote Updates

Public update feed for the private Blunote app.

This repository is meant to stay public so desktop clients can fetch update
manifests without authentication.

## Files

- `latest-mac.json`: macOS update manifest
- `latest-win.json`: Windows update manifest

## Manifest format

```json
{
  "version": "0.1.1",
  "url": "https://github.com/xiaomaolu/blunote-updates/releases/download/v0.1.1/Blunote-0.1.1-arm64.dmg",
  "notes": "Release notes"
}
```

## App URLs

macOS:

```text
https://raw.githubusercontent.com/xiaomaolu/blunote-updates/main/latest-mac.json
```

Windows:

```text
https://raw.githubusercontent.com/xiaomaolu/blunote-updates/main/latest-win.json
```

## Release workflow

1. Create a public GitHub repo named `blunote-updates`.
2. Push this directory to that repo.
3. Create a GitHub Release tag such as `v0.1.1`.
4. Upload release assets:
   - `Blunote-0.1.1-arm64.dmg`
   - `Blunote-0.1.1-arm64-mac.zip`
   - `Blunote-Setup-0.1.1.exe` if publishing Windows
5. Update `latest-mac.json` and `latest-win.json` to point to the release asset URLs.
6. Commit and push the updated manifest files.

## Current source build

- Source branch: `master`
- Source commit: `bc055f1`
