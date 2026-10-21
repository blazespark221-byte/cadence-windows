# Windows 1.2.15 release verification — 20 October 2026

Application source: 21ad23b7c03e52b49e4511dd4754d7d753838c8b in blazespark221-byte/cadence (branch fix/clipboard-images-windows, on top of 1.2.14 d6f11ee). 21ad23b keeps pictures on the clipboard instead of refusing to paste. The clipboard snapshot saves screenshots and pictures (DIB for CF_BITMAP/CF_PALETTE, enhanced metafile bits for CF_ENHMETAFILE/CF_METAFILEPICT) and restores them after dictation, Refine and Agent pastes. Data it cannot save (owner-display, private or GDI-object handles, delayed data an app fails to render, or beyond the size cap) is left out instead of blocking the paste; when nothing could be saved, the dictated text stays on the clipboard as a backup. The same commit bumps the version, adds the release notes and runs the new clipboard checks in CI.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39222188140

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.15-39222188140; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 203 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 78 portable parity checks; 302 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.14. It is not the shipping managed route.

Not tested: clipboard contents from real Office apps, image editors and screenshot tools on a desktop (the formats were placed natively by the checks), the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
