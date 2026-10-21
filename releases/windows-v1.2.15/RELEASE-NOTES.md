# Cadence for Windows 1.2.15 — dictation works with a picture on your clipboard

- **Dictation and Refine work when you've copied a screenshot, a picture or Office content.** Cadence used to stop with "Couldn't insert text: the clipboard contains an image or app-owned format". It now saves the picture, pastes your words and puts the picture back on your clipboard.
- If an app has put something on the clipboard that only it can provide (rare app-private data), Cadence pastes anyway and gives back everything else that was there. When nothing on the clipboard can be read, your dictated text stays on it as a backup.
- Includes dictation at the cursor from 1.2.14, Cadence in the notch by default from 1.2.13 and Cadence Agent voice conversation from 1.2.12.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
