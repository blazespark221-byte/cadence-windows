# Windows 1.2.20 release verification — 21 October 2026

Application source: e304a7b21d9a499f5e4b8ed3bdfd04bd0f4a3ebf in blazespark221-byte/cadence (branch fix/no-live-transcript-windows). 9f386ab removes the live transcript from the recording pill and the notch island: while recording they show only the destination icon and the waveform, and streaming partial results are no longer displayed. 9675bf0 merges 1.2.19 (03bbad2: Agent page, one-time move into the notch, rounded Refine buttons), which already contains 1.2.18 (70f4f73: account required, signed-in email) and 1.2.17 (89342e9: browser sign-in returns to Cadence, usage-limit wording). e304a7b bumps the version and adds the release notes. 1.2.20 was published as Latest before 1.2.17–1.2.19, at the owner's request; it contains all of them.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39559765463

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.20-39559765463; installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Executed on this candidate:
- 212 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including "Recording popup stays compact and keeps visible recovery without timer or Cancel".
- 79 portable parity checks; the managed-account suite (1855 checks reported); the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies (50 each), including "Render compact recording pill at reference height" and "Notch island stays in the notch band while recording (no live transcript)"; 489 packaged offscreen checks.
- 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 18 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs (commit, cancel, restart failure).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.16. It is not the shipping managed route.

Not tested: the popup during live microphone dictation on a physical Windows PC (the layout was checked in automated and packaged smoke checks, and the notch island was captured on screen on a development PC), the agent with the live AI service on Windows, fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
