# Cadence for Windows

Speak to insert text at your cursor, or select text, ask for a rewrite, review it and replace the selection.
Cadence runs in the Windows notification area and uses the original Cadence logo and dictation pop-up design.

[Download Windows 1.0.0 RC1](https://github.com/blazespark221-byte/cadence-windows/releases/tag/windows-v1.0.0-rc.1)

This is a **release candidate**, not a certified stable release. The remaining interactive editor test could not
run because Windows Search prevented the disposable test editor from becoming active. The build is unsigned.
Read the [verification record](VERIFICATION.md) for executed checks and the precise limits.

## Installation

Use `Cadence-1.0.0-windows-x64-setup.exe`, or extract the entire portable ZIP and open `Cadence.exe`.
The downloads include the required runtimes. No administrator account or developer tools are required.
The x64 build targets Windows 10 version 2004 and later; execution was verified on Windows 11 x64.
Compare the download with the accompanying `SHA256SUMS.txt` before running it.

Choose **Open Cadence** from the tray, then **Providers**. Configure speech and text separately using your own
provider credentials or compatible local services. Text generation also supports the separately installed
official Codex client. The app includes a microphone test, practice editor and connection checks.

- **Ctrl+Alt+Space:** start/finish dictation.
- **Ctrl+Alt+R:** rewrite selected text and review the result.
- **Escape:** cancel the current operation.

API keys use Windows DPAPI. Cadence preserves the clipboard and checks the destination before insertion.
Password fields, read-only fields and elevated applications are refused. Unconfirmed results remain recoverable.
Uninstall retains local settings and encrypted keys; the included README explains how to remove them.

## Verification

518 shared core checks, 39 bridge checks, 23 independent protocol checks, 38 Windows component/controller checks,
28 UI checks, and all seven final package/install/upgrade/uninstall checks passed. A real synthetic Codex rewrite
also passed. Native text anchors were checked against actual WPF UI Automation and native EDIT controls.
These component checks do not replace external-editor interaction, a clean OS matrix, or real provider speech accuracy testing.

This repository contains distribution files and documentation only. The application source is maintained separately.