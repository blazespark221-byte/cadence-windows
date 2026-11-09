# Cadence for Windows 1.2.52: fewer interrupted dictations

- **Dictation keeps everything you say after a long pause.** On a muted, noise-cancelling or virtual microphone that sends complete silence, words after a pause of about 20 seconds could be missing. Cadence's service now fixes this for every version, including this one.
- **A quick tap of the shortcut ends quietly.** Releasing the shortcut while the microphone was still opening showed a "Couldn't transcribe" card; now nothing happens, as with any dictation where nothing was said.
- **A stalled connection no longer leaves you on "Transcribing".** If the transcript hasn't arrived 15 seconds after you stop, Cadence sends your recording again instead of waiting for minutes.
- **A shortcut another app had taken comes back as soon as it's free.** Choose it again in Settings → Shortcuts and it works; the note beside it updates right away. If another app takes dictation's own shortcut, your other shortcuts keep working.
- **An old spoken-language setting no longer stops dictation.** A language Cadence doesn't list is now detected automatically instead of showing "Choose a supported spoken language".
- Your settings, sign-in, History and chats are kept. Includes all features from 1.2.51.

Includes the required runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for exact checks and remaining limits.
