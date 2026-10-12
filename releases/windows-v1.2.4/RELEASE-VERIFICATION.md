# Windows 1.2.4 release verification — 12 October 2026

Application source: 9c7033d69af80007814896f9d0e68b8b80dea5fc in blazespark221-byte/cadence (branch feature/agent-voice-mark-windows, on top of the 1.2.3 release record 1e34e4a).
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38242282032

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 178 Windows logic/controller checks, zero failures (one separate desktop suite excluded).
- 40 portable Cadence Agent, streaming and settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner.
- 424 offscreen UI checks and 402 synthetic renders, including the Cadence Agent window and progress card with the new character. Also 7 packaged floating-control input checks, 59 managed-writing/core bridge checks and 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.3. It is not the shipping managed route.

The character (AgentCharacter) was compile-checked on macOS and initialised offscreen on the runner; its motion constants mirror the Mac app, whose character was checked live on a Mac.

Not tested: the character on a real Windows desktop (frame pacing, the listening response to a real microphone, high-contrast and "Show animations" off), dictation into Google Docs or other browser editors on a real Windows desktop, a real-user browser sign-in from the welcome guide, the agent with the live AI service on Windows, production-identity installation, and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
