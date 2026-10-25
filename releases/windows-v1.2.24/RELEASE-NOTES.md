# Cadence for Windows 1.2.24 — dictation waits instead of failing when Cadence is busy

- **No more "Cadence is still finishing another request" after you've spoken.** Cadence handles one dictation at a time per account. If it's still finishing your previous one (for example after a dropped connection), your recording now waits and is sent as soon as Cadence is free. The pop-up says "Waiting for Cadence…" for up to about a minute.
- **Try again sends the same words.** If a dictation still can't be sent (Cadence busy, no connection or a service error), the message keeps your recording, and Try again sends it again instead of starting a new recording. The recording stays in memory only, until you dismiss the message or start something else.
- **A used-up Free allowance is reported straight away**, before you speak, instead of after the recording.
- Includes everything from 1.2.23: the simpler time-saved card on Home.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
