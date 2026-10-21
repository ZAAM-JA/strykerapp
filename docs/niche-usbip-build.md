# Niche VPN Kit — USB/IP Stability Test Build

This branch contains experimental USB/IP logging and process-exit diagnostics for StrykerOSS 6.5. The original `main` branch remains unchanged.

## Scope

- Reduced per-transfer USB/IP log flooding; aggregate transport errors.
- USB/IP server exit-status reporting.
- Debug build application ID: `com.zalexdev.stryker.nichetest`, so it does not replace the original Stryker installation.
- Linux guest network controller and NAT settings are **not** modified by these source changes.

## Building

GitHub Actions workflow: `.github/workflows/android.yml`.

On pushes to `niche-usbip-stability`, the workflow runs `./gradlew :app:assembleDebug --stacktrace --no-daemon` and, if successful, uploads the generated APK as a workflow artifact for 14 days.

Debug APKs are test-only, locally signed by the Android build system, and have separate app data from the original Stryker. Do not uninstall the working application or delete existing guest data for this test.

## Test objective

Investigate why Alfa AR9271 USB/IP and/or the UML runtime disconnect when transparently forwarding hotspot client traffic through an already-connected Android VPN. The first successful build is diagnostic only, **not** a verified fix.
