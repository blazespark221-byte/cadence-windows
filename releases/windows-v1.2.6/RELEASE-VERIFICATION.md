# Windows 1.2.6 release verification — 12 October 2026

Application source: 1e4713612be7086cb9a21a5842d975c6f7fc011c in blazespark221-byte/cadence (branch fix/google-docs-insert-windows-1.2.6, on top of 1.2.5 1c15d70 and 1.2.4 9c7033d).
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38244692669

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

Cause of the fix: a probe on the runner showed that Chrome 154 and Edge 153 keep Windows keyboard focus on their top-level `Chrome_WidgetWin_1` window rather than `Chrome_RenderWidgetHostHWND`, so the browser-page dictation path from 1.2.1 never engaged. Google Docs then went through the strict text-field anchor on its hidden input, which refused or could not confirm the paste.

Executed on this candidate:
- 10 new native browser dictation checks with real Chrome 154 and Edge 153 on the runner desktop, using Cadence's real capture and insertion while the default Ctrl+Alt+Space shortcut is held and the recording overlay is shown. A page modelled on Google Docs (canvas document, offscreen aria-hidden contenteditable that empties after each edit) receives the dictation as a paste-only target with no spacing guess. Another hidden-input editor is pasted into without read-back. An ordinary web text field keeps its verified anchor and smart spacing. Focus moved to the address bar is refused before any paste, and the address bar itself is not treated as page content.
- 178 Windows logic/controller checks, zero failures (one separate desktop suite excluded), including browser host and Google Docs/Slides title rules.
- 40 portable Cadence Agent, streaming and settings parity checks; 283 managed-account checks.
- 6 native Cadence Agent checks against real Notepad on the runner.
- 442 offscreen UI checks and 420 synthetic renders. Also 7 packaged floating-control input checks, 59 managed-writing/core bridge checks and 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.5. It is not the shipping managed route.

Not tested: real Google Docs (docs.google.com) on a Windows desktop — the runner used a page built like it, without a Google account; Firefox and Brave; a physical microphone session; the agent with the live AI service on Windows; a real-user browser sign-in from the welcome guide; production-identity installation; and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
