# Windows 1.2.49 release verification - 4 November 2026

Application and package source: `6fe15bc4a207c09102f5bbf7cc555e32de820dad` in `blazespark221-byte/cadence`, branch `release/windows-1.2.49`, based on Windows 1.2.48 (`364cdc1e`). Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/41819908242 (attempt 1, source unmodified). Exact candidate stored in the private draft release `windows-candidate-1.2.49-41819908242`.

This release makes Dictionary words that are heard as ordinary words ("fell" for fal) come out right. The shared CadenceCore code finds words that sound like a Dictionary term without being spelled as one, the cleanup prompt names them, and with cleanup off the bridge's new dictionary check asks the writing service about those words alone and keeps only its choice for them. S1-mini is skipped for such dictations. The same Core change shipped in Mac 0.3.43 (64).

Both the Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The package includes matching .NET Desktop/Swift runtimes and Microsoft.ML.OnnxRuntimeGenAI 0.18.0 (with the licences for S1-mini and ONNX Runtime GenAI). The downloaded ZIP and installer match the build's SHA-256 manifest; 531 payload files were independently verified against build-manifest.json. No application source or customer credentials are included in the public release.

Checks on this revision: 1889 managed-account checks; 131 portable parity checks; 913 CadenceCore checks (on a Mac), including the new dictionary checks.

Windows application acceptance: 243 logic/controller checks (0 failures; 1 separate desktop suite skipped), including two new checks that run the real bridge with cleanup off (a dictionary sound-alike is decided by the writing model and only that word changes; a dictation with none sends no writing request), 8 Annotate offscreen, 12 Chrome/Edge dictation, 5 opaque-editor, 11 native shortcut and 10 clipboard checks. Exact-package checks: 4 headless gates, 7 floating-control checks, and 16 isolated installer/lifecycle gates, including upgrade from 1.0.4, restart/reinstall, synthetic settings/encrypted-session retention, uninstall and updater handoffs. Verification installers use a separate identity and temporary profiles; the production installation is not changed by these checks.

Earlier CI runs of this release stopped on a parity check whose allowance fixture expired on 2 November 2026 (it read the real clock; fixed), the new dictionary-check diagnostics missing from the allowlist (fixed), and a clipboard check that deleted its folder while History still held it (fixed). The run above passed first time from this source.

The prompt and decision code were also run end to end against Gemini 2.5 Flash Lite from a Mac: cleanup on 27/27, cleanup off 26/27 test sentences, with no ordinary word replaced.

Remaining limits: the installer is unsigned. This build has only been run on CI runners and in local automated checks, not in everyday use on a real PC. The dictionary check has not been run with a physical microphone or against the live Cadence service from Windows. No live Ask Cadence, live Chat model, physical microphone dictation, Parakeet or S1-mini dictation on a laptop, fresh real browser sign-in, production-identity installation or real monitor/DPI transitions are certified here. The optional legacy Swift speech capability result is false; it is separate from the shipping on-device dictation path.

See verification-summary.json for exact machine-readable counts and flags.
