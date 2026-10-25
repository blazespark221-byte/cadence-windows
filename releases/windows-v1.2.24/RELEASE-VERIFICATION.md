# Windows 1.2.24 release verification — 25 October 2026

Application source: f850133bcf148a19be8202e4d10cbd79e5e43c46 in blazespark221-byte/cadence (branch fix/stuck-dictation-windows), stacked on 1.2.23 (959b4a3). Dictation no longer fails with "Cadence is still finishing another request" after the person has spoken.
- A live connection refused as busy (HTTP 429/402 on the upgrade) keeps recording.
- The completed recording waits for the service for up to about 75 s ("Waiting for Cadence…").
- A recording that still can't be sent is kept in memory, so Try again sends the same words.
- A cached Free plan with its dictation allowance used up stops the microphone at once.
- 5b90fba is the change and f850133 allowlists its four diagnostics.

The same day the cadence-api service was changed (version 3ead4e70): a live dictation now holds the account's single dictation place as a 60 s lease, renewed while the connection is active, instead of for up to 365 s.

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40186086547 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.24-40186086547. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

An earlier run on 5b90fba (40185323010) failed one check: the four new dictation diagnostics were not in the diagnostics allowlist. f850133 adds them; nothing else changed.

Executed on this candidate:
- 218 Windows logic/controller checks with zero failures (1 separate desktop suite skipped). These include the managed speech checks:
  - a busy service is waited out and the same recording is sent unchanged;
  - the daily limit is not waited out;
  - waits are bounded;
  - only failed sends (timeouts, no connection, 5xx, busy) are kept for Try again, never rejected audio or sign-in.
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 82 portable parity checks. They include a real loopback 429 refused upgrade through Windows' WebSocket client, the busy/resend policy and the kept-recording wording.
- The managed-account suite (1855 checks reported). The artifact verifier checked 512 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.23. It is not the shipping managed route.

Not tested: a real busy refusal from the live service with a real microphone on a physical Windows PC, Try again inserting into a real editor after a failed send, the agent with the live AI service on Windows, fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
