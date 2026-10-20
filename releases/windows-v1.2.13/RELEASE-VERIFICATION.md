# Windows 1.2.13 release verification — 20 October 2026

Application source: c16ea19c674f1bcad65e0048fb7e9ac688d7766d in blazespark221-byte/cadence (branch feature/notch-default-windows, on top of 1.2.12 2b77508 and its record c1217a9). dca9d7c starts fresh settings with the floating controls docked in the virtual notch at the top centre of the work area. Saved settings keep their edge, and settings saved before floating controls existed (1.0.x) keep the bottom glass tab. c16ea19 bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39225138769

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.13-39225138769; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 202 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 78 portable parity checks; 302 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 4 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.12. It is not the shipping managed route.

Not tested: the notch with a real pointer on a physical display, multi-display and high-DPI notch placement, full-screen hiding with real games, the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
