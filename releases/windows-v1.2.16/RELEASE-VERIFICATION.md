# Windows 1.2.16 release verification — 20 October 2026

Application source: 376f92eca7e39f7185fd6d1b2e6dafd2205d5bb2 in blazespark221-byte/cadence (branch fix/stuck-key-windows, on top of 1.2.15 21ad23b). e7385a8 keeps a stuck key from silently disabling lone-modifier shortcuts: when a bound lone modifier goes down, other keys silent for over 1.5 s are forgotten if Windows reports them up or they are not modifiers, while a silent modifier Windows still reports down keeps making a chord. Diagnostics logs "Shortcut · stuck key ignored" and "Shortcut · ignored: another key held". 376f92e bumps the version, adds the release notes and allowlists two 1.2.14 diagnostics.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39225110381

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.16-39225110381; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 208 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 78 portable parity checks; 302 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.15. It is not the shipping managed route.

Not tested: a key held by a real third-party tool on a physical keyboard (stale keys were simulated in the logic checks), the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
