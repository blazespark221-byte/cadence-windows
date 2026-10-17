# Windows 1.2.12 release verification — 18 October 2026

Application source: 2b77508101a7b4b5391bd980371fc6f55c1a1d51 in blazespark221-byte/cadence (branch release/agent-voice-windows, on top of 1.2.11 10d2d3d and its record 30033df). It merges feature/agent-beta-voice-windows (5ab3e96: Cadence Agent voice conversation with spoken replies through the Cadence service and talk-to-interrupt, the robot-on-top layout, the composer with attachments, Manual / Full access, dictation and voice mode, the step list, the Agent page in the main window, and the engine fix for repeated writes behind "HTTP 502"), and 2b77508 ports the Mac's retuned talk-to-interrupt thresholds.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39035379129

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.12-39035379129; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 202 Windows logic/controller checks with zero failures (one separate desktop suite skipped).
- 77 portable parity checks (including the agent voice, talk-to-interrupt, permission and engine checks); 302 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 4 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.11. It is not the shipping managed route.

Not tested: the agent's voice conversation with a physical microphone and speakers on Windows (spoken replies, talk-to-interrupt and hands-free turns were checked only with recorded levels), the agent with the live AI service on Windows, real Google Docs on a Windows desktop, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
