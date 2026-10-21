# Windows 1.2.18 release verification — 21 October 2026

Application source: 70f4f739fb83f5cb99da995b4d1b23ce571af425 in blazespark221-byte/cadence (branch fix/sign-in-required-windows, on top of 1.2.17 89342e9). 70f4f73 requires a Cadence account in the welcome guide (no Continue past "Your Cadence account" and no "Set up later" while signed out; signing out elsewhere sends an open guide back to that step), offers "Sign in" instead of "Try again" when a shortcut is refused for having no account, leads Home with "Sign in to start using Cadence", and shows "Signed in as <email>" in Settings → Account and the guide. The email is the verified primary address returned by POST /v1/auth/session, saved with the encrypted session; sessions saved by earlier versions ask once. 89342e9 (1.2.17) returns the starting window to the front when the browser hands the sign-in back.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39559036568

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was also kept as the private draft release windows-candidate-1.2.18-39559036568; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 212 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the signed-out and signed-in welcome-guide checks.
- 79 portable parity checks; 1855 managed-account checks, including the account-email checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- 471 packaged offscreen UI checks, including the signed-out account step, the signed-out Home and the "Signed in as" Account page.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 18 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

Before release, the deployed service was checked to refuse dictation, writing and model requests without an account (HTTP 401).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.16. It is not the shipping managed route.

Not tested: a real Google or email sign-in through the browser on Windows with this build, the email lookup against the live service for a session saved by 1.2.17 or earlier, the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
