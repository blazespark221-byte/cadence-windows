# Windows 1.2.0 release verification — 12 October 2026

Application source: 49421ac5cb7c22911935fabaea7108bd0fd9fdcf in blazespark221-byte/cadence (branch agent/cadence-agent-windows).
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38157996683
Exact-candidate revalidation: https://github.com/blazespark221-byte/cadence/actions/runs/38159525136

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 177 Windows logic/controller checks, zero failures (one separate desktop suite excluded).
- 19 Cadence Agent portable checks and 21 streaming/settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner: launch from the Start menu app list, UI Automation observation with element ids, Unicode typing and clipboard paste, Ctrl+A/Backspace, a scripted end-to-end agent run, and refusal of a stale element id.
- 418 offscreen UI checks and 396 synthetic renders; 7 packaged floating-control input checks; 57 managed-writing/core bridge checks; 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The first acceptance run reported the updater cancel-handoff fixture parent exiting 1 although its handoff report recorded a correct cancellation; the unchanged exact candidate then passed all 16 gates in the revalidation run. The optional legacy Swift bridge capability check also failed in the first run, as in 1.1.0 and 1.1.1; it is not the shipping managed route.

Not tested: the agent with the live AI service on Windows, Microsoft Word on Windows, real-user sign-in, physical microphone sessions, production-identity installation, and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
