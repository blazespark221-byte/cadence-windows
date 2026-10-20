# Cadence for Windows 1.2.14 — dictation goes where your cursor is

- **Dictation goes where your cursor is:** if you click into another field, the app redraws its text box, focus takes a moment to come back, or you switch to another app while Cadence is transcribing, your words are typed at the cursor instead of stopping with "Couldn't insert text". Cadence never types over a selection you didn't start with, into a password field or a blocked app; then your text waits for **Insert here** or **Copy** as before.
- **Dictation in apps that don't describe their text fields to Windows** (some games, Qt, Java and custom-drawn editors): Cadence pastes there and now leaves the text on your clipboard as a backup, because it can't check the result.
- Includes Cadence in the notch by default from 1.2.13, Cadence Agent voice conversation from 1.2.12 and faster dictation from 1.2.11.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
