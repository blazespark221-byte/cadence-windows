# Windows 1.2.2 release verification — 12 October 2026

Application source: a2589ecfd7a5a20c934e2bf79de88d69dd322c42 in blazespark221-byte/cadence (branch fix/cleanup-speed-windows, on top of the 1.2.1 release record 7682524).
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38222164915

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 178 Windows logic/controller checks, zero failures (one separate desktop suite excluded).
- 40 portable Cadence Agent, streaming and settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner.
- 424 offscreen UI checks and 402 synthetic renders. Also 7 packaged floating-control input checks, 59 managed-writing/core bridge checks (including the new Light cleanup skip: clean speech returns the exact original with no writing request, and `cleanupNeeded` answers locally for each level) and 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.1. It is not the shipping managed route.

The faster cleanup responses come from the Cadence service (deployed separately on 12 October 2026, version 754b214d), which applies to every Windows version. Server behaviour was checked with local Worker tests and live synthetic writing requests.

Not tested: Light cleanup on a real Windows desktop with a microphone (the skip decision is covered by bridge and Core checks), dictation into Google Docs or other browser editors on a real Windows desktop, a real-user browser sign-in from the welcome guide, the agent with the live AI service on Windows, production-identity installation, and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
