# Windows 1.2.21 release verification — 23 October 2026

Application source: 01ff69768542c98fec21bf6fb6e5cf61dcdf7cdf in blazespark221-byte/cadence (branch feature/sidebar-shortcut-windows), stacked on 1.2.20 (64f33f6). It makes the dictation shortcut in the main window's sidebar a button: click it, then press the new shortcut (a key combination, a lone Ctrl/Alt/Shift, or Mouse 4/5), and it saves at once. Escape or a second click keeps the old shortcut; a conflict with another app or with the rewrite/Agent shortcut is shown in the sidebar and the old shortcut stays. The capture rules now live in ShortcutCaptureRules/ShortcutCapture, shared with Settings → Shortcuts. The same commit bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/39926583422

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.21-39926583422; installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt after download. (The run's Actions artifact upload hit the storage quota; that step is allowed to fail, and the draft release holds the same files plus the verification evidence.)

Executed on this candidate:
- 215 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the three new shortcut capture rule checks.
- 11 native shortcut capture checks on the runner desktop (now part of the workflow), including the four new sidebar checks: click then Ctrl+Shift+K becomes the dictation shortcut and global shortcuts resume; Escape keeps the shortcut and focus; Mouse 5 becomes the shortcut; Mouse 4 (the fixture's rewrite shortcut) is refused, the old shortcut kept and no rewrite runs.
- 79 portable parity checks; the managed-account suite (1855 checks reported); the artifact verifier checked 512 payload files and 5 artifact hashes.
- Packaged smoke checks on the portable, installed and upgraded copies (50 each); 499 packaged offscreen checks, including "The sidebar shows the dictation shortcut as a button that changes it", "Clicking the sidebar shortcut waits for a new one" and "Clicking it again keeps the old shortcut" in light and dark.
- 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 8 native clipboard-format checks; 6 native Cadence Agent checks against real Notepad.
- 7 packaged floating-control input checks; 18 managed .NET speech checks with local services.
- Package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs (commit, cancel, restart failure).

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.20. It is not the shipping managed route.

Not tested: side buttons on a physical mouse (the checks use synthetic SendInput clicks), the sidebar on a physical Windows PC, the agent with the live AI service on Windows, fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
