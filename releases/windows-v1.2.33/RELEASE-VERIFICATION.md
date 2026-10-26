# Windows 1.2.33 release verification — 26 October 2026

Application source: acc1801da4d357f1c185ca29a53c9fdaf49df2f4 in blazespark221-byte/cadence (branch feature/ai-limits-windows), stacked on 1.2.29 (35199f2, record a4f16cb). 1.2.31 and 1.2.32 were built but not published on their own, so this release carries both:
- 1.2.31: Chat, Cadence Agent (including its spoken replies), Annotate and Translate send `X-Cadence-Feature` to the Cadence service, which gives them a shared weekly allowance (Free 20, Pro 1,000 fair use; cadence-api version 59ae47de). Dictation, dictation cleanup and Refine never send it. When the allowance runs out, Chat, Annotate, Translate and the Agent say so and when it resets, and the Agent stops at once. Settings → Account shows the weekly count (b66fce2, f5d3104).
- 1.2.32: Annotate and Translate capture the screen again. `Graphics.CopyFromScreen` throws for SourceCopy | CaptureBlt, so in 1.2.27 to 1.2.29 every attempt showed "Cadence couldn't capture your screen"; ScreenFreeze now makes the blit itself (7e00969, merged in 94b4915).
The 1.2.30 dictation level-meter fix is a separate line and is not included.

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40291867600 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.33-40291867600. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Earlier full runs on this line: the AI limits alone on 1.2.29 (b66fce2, run 40286228827, and f5d3104, run 40288660752) and the screen-capture fix alone on 1.2.29 (6f8415f, run 40291800001) all passed.

Executed on this candidate:
- 218 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 6 Annotate offscreen checks, including "Annotate copies a real part of the display, layered windows included", which reads a corner of the runner's real display (it fails on the 1.2.29 code with the shipped exception).
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 93 portable parity checks, including the spoken-reply request carrying `X-Cadence-Feature: agent`.
- The managed-account suite (1875 checks reported), including the weekly AI-feature refusal wording, plan decoding with and without the new usage fields, and Agent/Chat/Translate failure mapping. The artifact verifier checked 514 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, updater handoffs, and the installed smoke test, which now freezes the whole real display and presents the Annotate overlay over it.

Also run on this PC before the build: the bridge tests (78/78, including the feature tag on chat, generate and translation rewrite only), `--managed-controller-offscreen` (15/15, which `windows-managed.yml` doesn't run) and the app's `--offscreen-test` (569/569).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary in the installer step, as in 1.1.0 through 1.2.29. It is not the shipping managed route.

Not tested: Annotate and Translate on a physical Windows PC with a real mouse, real screens and multiple monitors; reaching the weekly AI-feature allowance with a real account against the live service; voice questions with a real microphone; fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
