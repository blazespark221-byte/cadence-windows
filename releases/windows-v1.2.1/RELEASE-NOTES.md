# Cadence for Windows 1.2.1 — Google Docs dictation and faster sign-in

- **Dictation in Google Docs and other browser editors:** Cadence now inserts dictation into Google Docs in Chrome, Edge, Brave and Firefox, and into other web or Electron editors that don’t expose their text to Windows accessibility. Previously these stopped with “Couldn’t insert text — focus an accessible text field”. Cadence still checks it is the same window, tab and app before pasting and still refuses password fields.
- **Sign-in goes straight to your browser:** the welcome guide’s account step now opens Cadence sign-in in your browser right away, with Sign in and Cancel in the guide itself, and moves on once you’re signed in. You no longer go through Settings → Account first.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
