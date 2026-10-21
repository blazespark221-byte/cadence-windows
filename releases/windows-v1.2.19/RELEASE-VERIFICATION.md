# Windows 1.2.19 release verification — 21 October 2026

Application source: 03bbad27c905839b24f74179853dab2befb9cab3 in blazespark221-byte/cadence (branch feature/agent-in-app-windows, on top of 1.2.18 70f4f73, merged in 462cbcb). 748cbb5 keeps Cadence Agent in the main window's Agent page: a request typed or spoken there runs and answers in the page (AgentPagePanel, sharing IAgentSurface with the request window), the window stays put while the agent works in the target app, and Cadence comes back to the front only for a Manual-mode OK or a typed question; the shortcut, notch, tray and floating controls keep the request window and progress card. 329baa9 moves every install's floating controls into the notch once (AppSettings.MovedToNotch). 3eb52d1 gives Refine's footer buttons the Mac's 9 px corners and a faint hover veil instead of the stock square chrome and blue hover. a1a2329 adds the Agent page renders to the offscreen checks and 03bbad2 bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39559056199 (attempt 2). Attempt 1 failed one of the 12 browser dictation cases (Edge, hidden-input page editor: the browser window with the probe page did not appear on its retry), with every earlier step passing; the job was re-run unchanged on the same source and all checks below passed.

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Actions artifact storage was full, so the passing candidate was kept as the private draft release windows-candidate-1.2.19-39559056199; installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Executed on this candidate:
- 212 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 79 portable parity checks; 1855 managed-account checks; the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.18. It is not the shipping managed route.

Not tested: a live Cadence Agent run from the Agent page on a real desktop (the page's request, steps and answer were checked only in offscreen renders; its Manual-mode approval was not exercised), Refine's hover with a physical pointer, the one-time notch move on a real upgraded profile beyond the packaged upgrade fixture, the agent with the live AI service on Windows, live microphone workflows, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
