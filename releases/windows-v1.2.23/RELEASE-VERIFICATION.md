# Windows 1.2.23 release verification — 25 October 2026

Application source: 3850a928cd79eba8febe072386f7d3c721a6fe3e in blazespark221-byte/cadence (branch feature/simple-time-saved-windows), stacked on 1.2.22 (174ad58). Home's time-saved card keeps its headline and replaces the time ruler and four-cell ledger with two speed bars (With Cadence and Typing, in words per minute) and one sentence ("2× faster than typing · 319 words · 5 dictations"). The Cadence speed uses the same clock as the time saved (start of speech until the text arrived, processing included), so the ratio matches the saving. The typing speed arrows sit on the Typing row. The same commit bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40102370683 (attempt 2)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.23-40102370683; installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Attempt 1 failed 2 of the 11 native shortcut capture checks (Settings shortcut fields: Shift+Tab and Escape did not leave capture on the runner desktop). This release does not change shortcut capture or Settings; the same commit passed all 11 on re-run (attempt 2).

Executed on this candidate (attempt 2):
- 215 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the offscreen render of Home in light and dark.
- 10 clipboard checks on the runner desktop; 11 native shortcut capture checks; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 79 portable parity checks, including the new check that the Cadence speed agrees with the time saved and is absent before any dictation; the managed-account suite (1855 checks reported); the artifact verifier checked 512 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.22. It is not the shipping managed route.

Not tested: the new Home card on a physical Windows PC (it was compiled and checked on a Mac, and rendered offscreen on the runner), the agent with the live AI service on Windows, fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
