# Windows 1.2.10 release verification — 14 October 2026

Application source: 7340d601470512d4b27c30ecd536102eb9bb21da in blazespark221-byte/cadence (branch feature/chat-windows, on top of 1.2.9 4ce2dcb and its record 30b4f6e). The change is 7538940 (the bridge's chat method and the shared CadenceCore chat engine), 263922b (Cadence Chat in the app), cde0e46 and 7340d60 (icon glyphs), dce1ee3 (Cadence Agent's new face) and f35aaa0 (the new interface sounds); 9756e93 sets the version.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38571458297

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

What changed:
- Cadence Chat: a chat window with saved chats and search, Markdown replies in a selectable document (headings, lists, tables, quotes, code with Copy), Stop, Try again, Regenerate and Copy. Files dropped on the window, the floating controls or the notch, or chosen with Attach, are read on the PC with the Refine readers (text, code, PDF text layers, Word .docx, OpenDocument, RTF; up to six per message) and only their text is sent. Entry points: Chat in the Cadence window's sidebar, Chat with Cadence in the tray menu, and a Chat button on the floating and notch controls. Settings → Privacy → Chat saves chats in %LOCALAPPDATA%\Cadence\chats.json (newest 300) and can delete them all.
- Replies go through a new bridge method, chat, which runs CadenceCore's ChatEngine, the same engine as the Mac app: the newest 40 messages that fit a 56 KiB request are sent as nonce-delimited turns, attachment text is bounded to 40 KiB per file and earlier files are left out first, with a note saying what was left out. Replies have their own cancellation lane, so dictation, Refine and Cadence Agent neither wait for nor stop them.
- Cadence Agent's character has bigger eyes and no mouth, as on the Mac. The five interface sounds are the Mac's new lower, warmer kit.

Executed on this candidate:
- 199 Windows logic/controller checks with zero failures (one separate desktop suite excluded), including a chat reply sent through the packaged engine with an attached file and earlier turns.
- 53 portable parity checks, 12 of them new for Chat: Markdown blocks matching CadenceCore, inline styles and safe links, titles, the bridge payload, saved chats (round trip, newest 300, one unreadable chat skipped, a corrupt file kept as .bak, delete), send and streamed snapshots, Stop keeping arrived text or offering Try again, failure and Regenerate, oversized messages, a deleted chat's late reply, and file limits.
- 66 managed-writing/core bridge checks, including 4 new chat checks: delimited turns with whole-reply snapshots, a cut-off reply kept and labelled, refusals and empty replies failing, and invalid conversations rejected before any network request.
- 463 offscreen UI checks and 438 synthetic renders, including the Chat window empty and with a reply (heading, list, table and code), files and a context note, in light and dark.
- 47 packaged smoke checks on each of the portable, installed and upgraded copies; 12 native browser dictation checks with real Chrome and Edge; 4 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 283 managed-account checks; 7 packaged floating-control input checks; 16 managed .NET speech checks with local services.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

The shared chat engine also passed CadenceChecks on macOS (1,014 checks), and Cadence Chat was used live on a Mac with the managed service: streamed replies, Markdown, and one message answered correctly from a text file, a Word file, a text PDF, a scanned PDF and a screenshot.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.9. It is not the shipping managed route.

Not tested: Chat on a real Windows desktop (opening it from the tray, notch and floating controls, dragging files from File Explorer, the Attach dialog, keyboard shortcuts); a chat reply through the live Cadence service on Windows; Agent's new face on a real screen (the offscreen renders draw it); the new sounds on real speakers; hovering the notch with a real pointer on the runner; real Office, LibreOffice and scanner files beyond the generated ones; real Google Docs on a Windows desktop; a physical microphone session; the agent with the live AI service on Windows; a real-user browser sign-in from the welcome guide; production-identity installation; and monitor/DPI transitions. Windows has no on-device text recognition in Chat or Refine, so images and scanned PDFs are refused with a suggestion. The installer is unsigned. No provider key or customer credential is embedded in these packages.
