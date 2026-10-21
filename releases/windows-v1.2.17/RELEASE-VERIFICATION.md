# Windows 1.2.17 release verification — 21 October 2026

Application source: 89342e98ccee350d19a132697777e3a32c7cc4b2 in blazespark221-byte/cadence (branch fix/sign-in-return-windows, on top of f36d71a, the usage-limit wording, over 1.2.16 376f92e). 89342e9 brings the window that started sign-in (the welcome guide or Settings → Account) back to the front when the browser hands the sign-in back. The short-lived callback process that the browser launches may take the foreground; before forwarding the callback over the current-user pipe it passes that right to the running Cadence (AllowSetForegroundWindow on the pipe server's process ID). f36d71a tells Pro and burst refusals apart from a used-up Free allowance and the daily cap. The "Cadence for Mac wants to access Cadence" page was Clerk's consent screen on the shared desktop OAuth client; it was turned off in the Clerk dashboard, not in this package.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39556737554 (attempt 4)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.17-39556737554; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 210 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the new browser hand-back check.
- 79 portable parity checks; 1,827 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 18 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

Attempts 1 to 3 of the same run each failed one different native browser case (an Edge probe window did not appear; a Chrome field read back before the paste landed; Edge focus left the page). Attempt 4 passed all 12. The same step passed on the first attempt in the 1.2.18 and 1.2.20 runs, which are built on this commit.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.16. It is not the shipping managed route.

Not tested: a real browser sign-in that returns to Cadence on a desktop (the foreground hand-off was checked through the pipe with a local listener), the Clerk consent-screen change, the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
