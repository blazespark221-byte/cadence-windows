# Cadence for Windows 1.0.5 — verification

Verified 5 October 2026 (Australia/Adelaide), Windows 11 x64 build 26200. Binary source: `a0abff852e674e9c3ec42d34d3c4f9306a2c7897`, clean committed source in the private Cadence repository. Shell and Swift bridge were built together; required runtimes are bundled. Frozen Core Contracts and Support were unchanged.

## Executed checks

- Windows Release build: zero warnings/errors. Shared Swift logic: 677 passed.
- Managed account: 283 passed. Billing: 17 passed. Windows logic/controller: 172 passed; one intentionally excluded desktop suite.
- Browser callback/sign-in lifetime: 9 synthetic checks passed. Managed controller: 13 passed.
- Artifact verifier: 512 payload files and five build-artifact hashes matched. Thirteen verifier regressions passed.
- Installer/updater tooling: 56 Node checks passed; one nonapplicable platform check skipped.
- Exact packaged UI: 362 checks and 345 offscreen renders passed at 100/150/200-percent render scales.
- Exact packaged managed speech: 16 passed, including real Windows HTTP upload at five minutes, cancellation and both speech roles. Exact packaged Swift writing/core: 51 passed, with its declared managed-app scope.
- Disposable cross-process editor: 7 passed, covering selected replacement/Undo, caret insertion, changed selection/field refusal, English/CJK spacing and clipboard restoration.
- Native Refine controller: 5 passed, covering selected replacement, caret composition, regeneration, late-result cancellation and changed-selection recovery.
- Package lifecycle: 16 passed, zero failed. Verified 1.0.4 → 1.0.5 upgrade under a separate verification installer identity, installed/reinstalled runtime launch, unchanged synthetic preferences and encrypted session bytes, and owned uninstall.
- Real updater helper: commit, cancellation and injected restart-failure rollback passed using the exact candidate and isolated installation. This helper test uses the same candidate version on both sides; the separate direct-installer test establishes upgrade from 1.0.4.
- Production application files, registrations, OAuth association, startup, shortcuts, settings and encrypted sessions were unchanged by all installer fixtures.

## Scope and remaining limits

The feature reference is the exact 1 October 2026 Mac source snapshot. Windows uses native Windows frames, notification-area controls and Windows key bindings. Offscreen render scales do not establish native multi-monitor/DPI behavior.

The full legacy Swift bridge suite separately failed at the five-minute WAV upload with a transcription timeout. This result is retained as a failure, not converted into a pass or omitted. The shipping managed app routes speech through .NET; the packaged .NET maximum-upload test passed. Writing and cleanup use the packaged Swift bridge and passed their checks.

Fresh real browser sign-in/consent, full microphone → live service → insertion workflows, production-identity installer execution, updater handoff between distinct application versions, native monitor transitions, sleep/resume, long sessions, other Windows versions, ARM emulation and broader editor compatibility were not verified in this release pass. No payment or production service setting was changed. Test fixtures used synthetic data. Prior synthetic-audio live-service results are historical evidence and were not counted as newly executed checks here.

The installer is unsigned; hashes establish byte identity, not publisher signing. The portable ZIP and installer contain build-time VERIFICATION.md; this later release record reports checks executed after packaging without altering those immutable package bytes.
