# Windows 1.2.7 release verification — 14 October 2026

Application source: e00d3608bf9eb37fc68d9906c825c380aa735f8b in blazespark221-byte/cadence (branch fix/windows-target-capture-1.2.7, on top of 1.2.6 4c9ba6d). The app change is 0757d00; e00d360 and 602a741 change only the browser check harness.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38553132137

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Cause of the fix: a user with Right Alt alone as the dictation shortcut saw “Couldn’t start recording · Target capture: focus an accessible text field” on every other press, and finished dictation waiting for Insert here. The low-level hook passed the lone Alt release to the app, and Windows treats a lone Alt tap as a menu command: Chrome and Edge move focus to their app menu button and the next lone Alt moves it back, and Win32 apps enter menu mode. Cadence now swallows that release and replays it behind the unassigned key VK 0xE8, so no menu opens. Dictation also pastes into desktop editors that UI Automation reports only as a bare Pane, Custom, Group or Window element (Mac parity), as a paste-only target; buttons, menus, lists, tabs, links, password, disabled and read-only fields are still refused.

Executed on this candidate:
- 12 native browser dictation checks with real Chrome 154 and Edge 153 on the runner desktop. New: in each browser, a lone Right Alt tap with no Cadence listener blurred the page’s text field (the reported bug, reproduced), then with Cadence’s real low-level hook and a tap-mode Right Alt binding, the start press captured the field, neither the start nor the stop press blurred it, and the dictation was pasted. The 10 checks from 1.2.6 (Google Docs-like canvas editor, hidden-input editor, ordinary text field, address-bar refusals) also passed. The harness now gives a case one fresh-browser retry; one case (Chrome, Google Docs-like editor) passed on its retry after a three-second accessibility timeout. Earlier runs 38549763386 and 38551209307 failed pre-existing cases for the same runner reasons (a click missing a freshly started browser, pastes read after the clipboard was restored); the Right Alt case passed in Chrome in 38551209307.
- 4 new native opaque-editor checks in an in-process window: a custom-drawn editor exposing only a Custom element receives dictation by paste; rewrite capture of it is refused; a focused button is refused; focus moved to a button after capture refuses insertion before pasting.
- 180 Windows logic/controller checks, zero failures (one separate desktop suite excluded), including the Alt mask rules and sequence and the editor-surface rules.
- 40 portable Cadence Agent, streaming and settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner.
- 442 offscreen UI checks and 420 synthetic renders. Also 7 packaged floating-control input checks, 59 managed-writing/core bridge checks and 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.6. It is not the shipping managed route.

Not tested: the fix on the reporting user’s PC or with a physical keyboard (the runner injects keys); Win32 menu-bar apps, Office and Firefox with an Alt shortcut; real third-party custom-drawn editors (the opaque-editor checks use a stand-in); real Google Docs (docs.google.com) on a Windows desktop; a physical microphone session; the agent with the live AI service on Windows; a real-user browser sign-in from the welcome guide; production-identity installation; and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
