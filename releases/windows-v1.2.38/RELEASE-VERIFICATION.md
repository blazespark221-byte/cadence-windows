# Windows 1.2.38 release verification — 27 October 2026

Application source: 388d082107c03ba3874734098fc577d384317b7f in blazespark221-byte/cadence (branch release/windows-1.2.38), stacked on 1.2.35 (ff13db2, record e7ad6d6). One release for everything built since 1.2.35; 1.2.30, 1.2.36 and 1.2.37 were reserved for parts of it and were never published on their own:
- Cadence Agent's model (agent-models-windows 21c86a6…72fc8b6): GPT-6 Luna (`cadence-chat`, every plan) or Claude Opus 5.5 (`cadence-chat-advanced`, Pro), only for Agent requests on the Cadence account. Live voice through GPT-Live (`/v1/agent/live`, docs/agent-live/CONTRACT.md), on by default for signed-in accounts, with the standard voice as the fallback.
- Agent connectors (agent-connectors-windows 1f2b7fc, docs/agent-connectors/DESIGN.md): email.compose, custom MCP connectors (Streamable HTTP; no auth, API key or MCP sign-in) and Settings → Connectors. The Gmail and Outlook OAuth client ids are empty in this build, so their rows say sign-in isn't set up and their tools are never offered.
- Home says how many times faster than typing (times-faster-windows 76ddf2b), Translate language search over 108 languages (translate-search-windows 6af5729), the launch "Update available" pop-up (update-popup-windows bc974b2), the adaptive dictation level meter (eb9e0be) and the Agent's microphone level drawn as the pill's bars (0f21b5d).
- Release fixes: an offscreen-check variable clash between the Styles and Agent-meter checks (5a7d63c), and a race in the live-voice barge-in parity check that read the fake socket before the send loop had delivered the loud frames (388d082, test-only; it failed once in run 40476302214).

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40477039743 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.38-40477039743. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Executed on this candidate:
- 230 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the update pop-up checks.
- 7 Annotate offscreen checks, including the Translate language search.
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 169 portable parity checks, including the Agent model aliases, the live-voice protocol through a fake socket and a loopback WebSocket upgrade, and the connector checks (Gmail/Outlook wording, MCP sessions, loopback sign-in).
- The managed-account suite (1882 checks reported). The artifact verifier checked 514 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, updater handoffs and the installed smoke test.

Also run on this PC before the build: the parity checks (169/169, three runs), the managed-account checks (1882), `Cadence.Windows.Checks --logic-only` (205 passed, 1 skipped), `--updater` (38/38), `--connectors-offscreen` (1/1), `--update-prompt-offscreen` (6/6), `--annotate-offscreen` (7/7) and the app's `--offscreen-test` (632/632), whose render of the Agent page while listening (model button, voice-level bars) was inspected. Before the merge, the live-voice session code ran against the real GPT-Live service with synthesized speech.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary in the installer step, as in 1.1.0 through 1.2.35. It is not the shipping managed route.

Not tested: live voice with a real microphone and speakers (echo gating, barge-in, output device changes), real Gmail, Outlook or MCP sign-ins and real MCP servers, the update pop-up and the Translate search on a physical desktop, and a real microphone for the level meter; fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
