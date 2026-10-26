# Windows 1.2.34 release verification — 26 October 2026

Application source: 0517a6a11b191f41aa70203129ea7dbd4b09b292 in blazespark221-byte/cadence (branch fix/annotate-pen-windows), stacked on 1.2.33 (acc1801, record c688d71). The one change: Annotate and Translate no longer hide the mouse pointer or draw a glowing rainbow ring in its place, so the ordinary pointer stays as it is while you circle something (d733765, 4099801). Drawing, the rainbow stroke, its glow and the sparkles are unchanged. The 1.2.30 dictation level-meter fix is a separate line and is not included.

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40299332534 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.34-40299332534. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Executed on this candidate:
- 218 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 6 Annotate offscreen checks, including a copy of a corner of the runner's real display and renders of the overlay in its ready, drawing, circled, listening, nothing-found and Translate states, now without the pen ring.
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 93 portable parity checks.
- The managed-account suite (1875 checks reported). The artifact verifier checked 514 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, updater handoffs, and the installed smoke test, which freezes the whole real display and presents the Annotate overlay over it.

Also run on this PC before the build: the Annotate offscreen checks (6/6) and the app's `--offscreen-test` (569/569).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary in the installer step, as in 1.1.0 through 1.2.33. It is not the shipping managed route.

Not tested: Annotate and Translate on a physical Windows PC with a real mouse, real screens and multiple monitors; voice questions with a real microphone; fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
