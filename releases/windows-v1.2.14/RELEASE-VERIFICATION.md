# Windows 1.2.14 release verification — 20 October 2026

Application source: d6f11ee757a0e7504d152d0fbfe57b9fefe7d754 in blazespark221-byte/cadence (branch feature/insert-anywhere-windows, on top of 1.2.13 c16ea19, merged in a69b7ed). a4e3db3 ports the Mac 0.3.15 caret follow: when the destination changed before anything was pasted, Cadence captures the caret again and inserts there (another field, or another app the user moved to while Cadence transcribed), looking for up to 1.5 s across up to 6 destinations. It never types into a selection it did not start with, a password, read-only or blocked field, or Cadence's own windows. A paste into an editor surface Windows cannot read leaves the text on the clipboard as a backup. d6f11ee bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39225368315

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.14-39225368315; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 203 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 78 portable parity checks; 302 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.13. It is not the shipping managed route.

Not tested: following the caret across real third-party apps with a physical microphone (the follow rules were checked in the logic suite, the opaque-editor native check and two full-controller cases), games, Qt and Java editors on a real desktop, the agent with the live AI service on Windows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
