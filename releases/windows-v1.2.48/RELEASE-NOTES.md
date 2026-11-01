# Cadence for Windows 1.2.48: History

- **History:** every dictation on this PC is now listed on the new History page, with the app it went to and the time. Search by words, app or window title, filter by app, copy a dictation or delete it. History starts with this version, so earlier dictations aren't there. It stays on this PC, is kept until you delete it, and can be turned off in Settings.
- **Dictating into terminals is more reliable:** Windows Terminal, the console, PowerShell, cmd and WSL no longer fail with "Couldn't start recording" or "Check your editor" when their output updates. Cadence pastes into them, and the text stays on the clipboard as a backup.
- **Tauri and other WebView2 apps:** dictation and Refine now work in them (this is the fix from 1.2.47, which wasn't published on its own).
- **The Claude Code sessions section is gone** from the sidebar. Cadence no longer looks at Claude Code sessions on this PC.
- Your settings, sign-in and chats are kept. Includes all features from 1.2.46.

Includes the required runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for exact checks and remaining limits.
