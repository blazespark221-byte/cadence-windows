# Windows 1.2.29 release verification — 26 October 2026

Application source: 35199f21d759060031fc3700c77a19c6bb376abb in blazespark221-byte/cadence (branch feature/no-release-notes-windows), stacked on 1.2.24 (6cf5243). 1.2.25 to 1.2.28 were built but not published on their own, so this release carries all of them:
- 1.2.25: the six-step welcome guide and the microphone test (3ea3976).
- 1.2.26: Chat opens out of the notch (4e08ad4, 0a0a2ac).
- 1.2.27: Annotate and Translate. Circled screen text is read on the PC by Windows.Media.Ocr and sent to Chat (Annotate) or the rewrite service (Translate) as text; the screen picture is never uploaded. The app now targets net8.0-windows10.0.19041.0.
- 1.2.28: the quieter graphite look with Segoe Fluent icons.
- 1.2.29: the Release notes button is removed from the update control (053e9f3).

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40284060848 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.29-40284060848. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Earlier full runs on this line: 1.2.26 (0a0a2ac, run 40262847841) and 1.2.27 with Annotate only (b5c86b2, run 40264070303) both passed. GitHub Actions refused jobs for billing reasons between those runs and this one, so 1.2.27 with Translate and 1.2.28 had no run of their own; this run covers both.

Executed on this candidate:
- 218 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 5 Annotate offscreen checks: Windows text recognition reads a synthetic quiz, an empty area returns no text, and the overlay, the translate hand-off and the translation card render.
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 93 portable parity checks, including the Annotate and Translate rules (loop detection, crop, question box placement, attachment text, shortcut defaults and the hand-off to Chat).
- The managed-account suite (1855 checks reported). The artifact verifier checked 514 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary in the installer step, as in 1.1.0 through 1.2.24. It is not the shipping managed route.

Not tested: Annotate and Translate on a physical Windows PC with a real mouse, real screens and multiple monitors; voice questions with a real microphone; the notch chat with the live AI service; the welcome guide's microphone test with a real microphone; fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
