# Windows 1.2.22 release verification — 24 October 2026

Application source: d74cdd1d0ac31508960e4f34378efee50952d35f in blazespark221-byte/cadence (branch feature/auto-copy-windows), stacked on 1.2.21 (ef01ebd). When dictation or a Refine result can't be inserted, Cadence copies the text to the clipboard straight away (after the insertion has put the previous clipboard back), and the recovery card or Refine notice says it can be pasted with Ctrl+V. Unconfirmed insertions also leave the text on the clipboard; a dictation whose cleanup didn't finish is not copied. Insert here, Retry insertion and Copy are unchanged. The same commit bumps the version and adds the release notes.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40091829493

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.22-40091829493; installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Executed on this candidate:
- 215 Windows logic/controller checks with zero failures (1 separate desktop suite skipped).
- 10 clipboard checks on the runner desktop, including the two new ones: "A failed dictation insertion copies the text for Ctrl+V" (the real controller's recovery card; an unfinished cleanup leaves the clipboard alone) and "An unconfirmed insertion also leaves the text on the clipboard".
- 11 native shortcut capture checks; 12 native browser dictation checks with real Chrome and Edge; 5 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 79 portable parity checks; the managed-account suite (1855 checks reported); the artifact verifier checked 512 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater handoffs.

On a development PC, the same source passed the 10 clipboard checks (the user's clipboard was restored afterwards) and 193 logic checks.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.21. It is not the shipping managed route.

Not tested: a real failed insertion followed by Ctrl+V on a physical Windows PC (the native full-controller checks that cover the Refine and caret-follow cases were updated but run only on an interactive desktop), the agent with the live AI service on Windows, fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
