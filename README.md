# Stardew Eden DS

Dual-screen integration for the Nintendo Switch version of Stardew Valley running in
[Eden DS](https://github.com/JoeCorrell/Eden-DS) on the AYN Thor.

This repository contains only the Stardew-specific patch and build automation. It does not
redistribute Eden, Stardew Valley, game assets, firmware, keys, ROMs, or save data.

## Current stage

The calibration build:

- detects Stardew Valley by title ID `0100E65002BB8000`;
- routes the companion interface to the lower display;
- reads and displays the exact main-module Build ID;
- provides the native snapshot bridge and initial HUD layout;
- keeps live guest-memory reads disabled until a verified build-specific profile is added.

This fail-closed behavior prevents unknown game updates from being interpreted using invalid
memory offsets.

## Build an APK

1. Open the **Actions** tab.
2. Select **Build Stardew Dual Screen APK**.
3. Choose **Run workflow**.
4. When the job completes, download the `Eden-DS-Stardew-calibration` artifact.

The workflow downloads the pinned Eden DS source, applies
`patches/stardew-dualscreen.patch`, and builds the dual-screen Android APK. The resulting APK
contains no game files.

## Install on AYN Thor

Enable wireless debugging or connect the Thor by USB, then run:

```bash
adb install -r app-dualscreen-relWithDebInfo.apk
```

The package is based on Eden DS's dual-screen flavor. Back up emulator configuration and saves
before replacing any existing test build.

Launch Stardew Valley and load a save. The lower screen will show the detected Build ID. The same
identifier is written to `Eden_Log.txt`. That value is required for the next calibration stage.

## Upstream base

The patch is intentionally pinned to Eden DS commit:

```text
dbe6b5c66bf9bdcf6667ab383ea6193f7ebaf7f9
```

When the upstream base changes, the patch must be reviewed and regenerated instead of being
applied blindly.

## License

The integration patch is licensed under GPL-3.0-or-later, matching Eden DS. Stardew Valley and
related assets remain the property of their respective owners.
