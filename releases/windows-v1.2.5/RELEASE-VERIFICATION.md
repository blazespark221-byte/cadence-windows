# Windows 1.2.5 release verification — 12 October 2026

Application source: 1c15d7046ca5ca9addb88d35034a10e1f2ac5b72 in blazespark221-byte/cadence (branch feature/weekly-allowance-windows, on top of the 1.2.4 source 9c7033d).
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38243680033

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 178 Windows logic/controller checks, zero failures (one separate desktop suite excluded).
- 40 portable Cadence Agent, streaming and settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner.
- 442 offscreen UI checks and 420 synthetic renders, including the new weekly dictation card at the top of Home (free, spent and Pro, light and dark). Also 7 packaged floating-control input checks, 59 managed-writing/core bridge checks and 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.
- 18 billing checks (run on macOS against the same source), including the weekly counter's words-left, overage clamp and recording-minutes cap.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.4. It is not the shipping managed route.

The weekly card reads the same server account status (/v1/account) as Settings → Account. The Mac app's identical card was checked live with a signed-in Pro account.

Not tested: the weekly card on a real Windows desktop with a signed-in free account (refresh after a live dictation, at the weekly reset and on window activation), dictation into Google Docs or other browser editors on a real Windows desktop, a real-user browser sign-in from the welcome guide, the agent with the live AI service on Windows, production-identity installation, and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
