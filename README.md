# Enable Screenshot — One UI 9 fork

Fork of [LSPosed/DisableFlagSecure](https://github.com/LSPosed/DisableFlagSecure) focused on restoring screenshot and screen-record behavior on Samsung One UI 9 / Android 17 while retaining the upstream hooks for older supported Android versions.

The module enables screenshots in apps that normally block them and disables screenshot detection on Android 14+ and screen-record detection on Android 15+.

## One UI 9 / Android 17 fixes

- Uses `android.window.ScreenCaptureInternal$ScreenshotHardwareBuffer` when the framework has migrated away from `ScreenCapture$ScreenshotHardwareBuffer`.
- Hooks `containsSecureLayers()` in both `system_server` and the screenshot/SystemUI process where available.
- Falls back from `VirtualDisplayAdapter.createVirtualDisplayLocked()` to `DisplayManagerService.createVirtualDisplayLocked()` when the adapter method is absent.
- Locates the virtual-display flags parameter by signature instead of assuming the first integer after the caller UID is the flags field.
- Accepts the known Samsung screenshot-target method names `canBeScreenshotTarget` and `isCaptureTarget`, restricted to boolean-returning methods.
- Keeps screenshot and screen-record detection hooks used by current Android releases.

The Android 17 changes were audited against Samsung Galaxy S25 Ultra One UI 9 Beta 2 firmware `S938BXXUCZZI4`. Other Android 17/OEM combinations are not claimed as tested by this fork.

## Supported OSes

- Android 12-16: upstream behavior retained.
- Android 17: Samsung One UI 9 compatibility additions in this fork.
- Xiaomi HyperOS and OPlus OS hooks are retained from upstream.

## Usage

1. Install the APK.
2. Enable the module in LSPosed.
3. Select **only** the recommended scopes.
4. Reboot, or use LSPosed hot reload when supported.

## Releases

GitHub Actions contains only a manually dispatched release workflow. It builds a signed release APK, verifies its package/version/signature, generates a SHA-256 file, and publishes both to GitHub Releases.

Required repository secrets:

- `GPR_USER`
- `GPR_KEY`
- `KEYSTORE_BASE64`
- `KEYSTORE_PASSWORD`
- `KEY_ALIAS`
- `KEY_PASSWORD`

The project does not run an automatic Android CI workflow on pushes or pull requests.
