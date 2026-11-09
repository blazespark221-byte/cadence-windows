# Windows 1.2.52 release verification - 9 November 2026

Application and package source: `d8c28a802d839bb72308f5243d3a2128375cc6d0` in `blazespark221-byte/cadence`, branch `release/windows-1.2.52`, based on Windows 1.2.51 (`0c573b11`). Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/42575913808 (attempt 1, source unmodified). Exact candidate stored in the private draft release `windows-candidate-1.2.52-42575913808`.

This release comes from a full production audit of 1.2.51 on 9 November 2026 (code review of the dictation, shortcut and account paths, plus live probes of the production service). Fixed in the Windows shell (`bfaf502c`):

- A tap released while the microphone was still opening sent no audio; `ManagedStreamingSpeech.Finish` failed it as "No audio was captured" and the user got a "Couldn't transcribe" card. It now ends as `NoSpeechException`, and `CanRecover` lets that verdict through, so a dropped, busy or failed stream with a short or silent recording also ends quietly.
- Once the finish frame starts, the final has 15 s (`FinalTimeout`; measured ~0.6 s in production). After it the stream ends as a recoverable timeout and the completed recording is uploaded, instead of waiting out the 340 s lifetime on a stalled connection.
- A shortcut left off because another app owned it is registered again on every settings save (`HasShortcutProblems`), so re-picking the same combination takes it back; the Shortcuts notes refresh after each save. Another app owning dictation's own combination now leaves only dictation off (`Register` accepts a null dictation binding) instead of every shortcut.
- `LanguageHint` sends only a listed language code; an unlisted saved value (an old free-typed "English") is detected instead of failing the stream.

Service change in the same audit (cadence-api `700c9fce`, rollback `9392be15`, all clients): Scribe v2 Realtime dropped all speech after a long run of exact-zero samples (muted, noise-gated or virtual microphones). Measured against the Gateway: 30 s of digital silence between two sentences lost the second; any noise floor, even ±1, kept it. The service now gives exact zeros a ±1 floor before forwarding. Verified in production after deployment.

CadenceCore, the Swift bridge, the packaging tools and the installer are unchanged from 1.2.51. Both the shell and the bridge were still built fresh from clean source on an isolated Windows x64 runner. The downloaded ZIP and installer match the build's SHA-256 manifest.

Checks on this revision: 1889 managed-account checks; 120 portable parity checks (4 new: listed-language hint, no-audio tap, short/silent recovery, final timeout). Windows application acceptance: 243 logic/controller checks (0 failures; 1 separate desktop suite skipped), 8 Annotate offscreen, 12 Chrome/Edge dictation, 5 opaque-editor, 13 native shortcut (one new: another app owning dictation's shortcut leaves the others working, and re-picking it takes it back) and 10 clipboard checks. Exact-package checks: 4 headless gates, 7 floating-control checks and 16 isolated installer/lifecycle gates, including upgrade from 1.0.4, restart/reinstall, settings/encrypted-session retention, uninstall and updater handoffs. The same workflow on the unchanged 1.2.51 source passed earlier the same day (run 42571108491).

Remaining limits: the installer is unsigned. Production-identity installation, physical microphone dictation and real monitor/DPI transitions are not certified here. The optional legacy Swift speech capability result is false; it is separate from the shipping dictation path.

See verification-summary.json for exact machine-readable counts and flags.
