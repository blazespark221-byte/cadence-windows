# Windows 1.2.11 release verification — 17 October 2026

Application source: 10d2d3d9d6c10ddc46f9c7f457c17e09030f12b5 in blazespark221-byte/cadence (branch feature/fast-cleanup-windows, on top of 1.2.10 7340d60 and its record 951acb3). It carries the unreleased quiet no-speech and waveform work from fix/quiet-no-speech-windows, the claude/speed-windows pass (the live dictation stream opens while the start sound plays, the writing connection is warmed, sign-in refreshes early, ReadyToRun start-up) and 9c9513e (on-device Light cleanup: the bridge's cleanupNeeded returns the cleaned text when the only issue is an English um/uh/erm or a stuttered short word, so no writing request is made). db0174b and 10d2d3d change only the notes and the workflow.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38994561120

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.11-38994561120; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 200 Windows logic/controller checks with zero failures (one separate desktop suite excluded).
- 59 portable parity checks; 302 managed-account checks; 57 artifact-verifier checks.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 4 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The on-device cleanup rules are shared with the Mac (CadenceChecks 1,091 passed on macOS) and were checked against 141 real dictation transcripts: 71% now insert without a writing request (62% before).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.10. It is not the shipping managed route.

Not tested: a physical microphone dictation on Windows with this build (so the measured speed-up and the on-device cleanup were not observed live), real Google Docs on a Windows desktop, the agent with the live AI service on Windows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
