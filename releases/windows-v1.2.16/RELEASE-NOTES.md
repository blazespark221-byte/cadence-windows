# Cadence for Windows 1.2.16 — a stuck key can't switch off your shortcut

- **Your Right Alt (or other lone Ctrl, Shift or Alt) shortcut keeps working when Windows thinks another key is still held.** If another app loses a key release, Windows can report a key such as F9 as pressed for hours. Cadence then treated every press as part of a key combination and did nothing. It now ignores a key that has stopped sending input. Real combinations such as Ctrl + Right Alt still cancel, and the lone Alt still doesn't open app menus.
- **Settings → Diagnostics now explains an ignored shortcut press** ("Shortcut · ignored: another key held" or "Shortcut · stuck key ignored"), and shows dictation events that used to appear as "unrecognized event omitted".
- Includes dictation with a picture on your clipboard from 1.2.15, dictation at the cursor from 1.2.14 and Cadence in the notch by default from 1.2.13.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
