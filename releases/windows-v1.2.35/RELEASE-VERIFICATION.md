# Windows 1.2.35 release verification — 26 October 2026

Application source: ff13db236891fc98c1ff551bf3b793de99896cbd in blazespark221-byte/cadence (branch feature/styles-windows), stacked on 1.2.34 (0517a6a, record e4f2028). The change: Styles. A person makes a style per audience (a name, optional tone notes and up to 20 example messages they really sent), and while one is chosen each plain dictation is rewritten in that voice instead of getting the cleanup pass. CadenceCore's DictationStyle and stylePrompt (2b1285f, shared byte-for-byte with Mac 0.3.29) build the prompt in the Swift bridge's `rewrite` method, which refuses a style combined with cleanup, Refine instructions, files, a target language or a feature tag (7223bba). The app adds the Styles settings, the Style chips in the notch, a Styles page in the main window, a tray picker, the style name in the dictation popup, and the same raw-transcript recovery as a failed cleanup (e56418a). A styled dictation is an untagged writing request, like cleanup. The 1.2.30 dictation level-meter fix is a separate line and is not included.

Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/40318615986 (attempt 1)

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. The passing candidate was kept as the private draft release windows-candidate-1.2.35-40318615986. The installer, portable ZIP and manifest hashes were checked against SHA256SUMS.txt and the artifact manifest after download.

Executed on this candidate:
- 224 Windows logic/controller checks with zero failures (1 separate desktop suite skipped), including the Styles settings checks and real-bridge controller checks for a styled dictation, the Off paths and a failed style rewrite.
- 6 Annotate offscreen checks.
- 10 clipboard checks on the runner desktop, 11 native shortcut capture checks, 12 native browser dictation checks with real Chrome and Edge, 5 native opaque-editor checks, and 6 native Cadence Agent checks against real Notepad.
- 98 portable parity checks (5 new for Styles).
- The managed-account suite (1875 checks reported). The artifact verifier checked 514 payload files and 5 artifact hashes.
- Exact packaged headless runtime gates (4 passed) and 7 packaged floating-control input checks.
- Package and lifecycle gates on the exact candidate (16 passed): isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, updater handoffs and the installed smoke test.

Also run on this PC before the build: the CadenceCore checks (795/795, 6 new for the style prompt, limits and output filter), the bridge tests in the managed-app scope (73/73, 3 new for Styles) and the app's `--offscreen-test` (617/617), whose renders of the Styles page, the notch Style row and the dictation popup were inspected.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary in the installer step, as in 1.1.0 through 1.2.34. It is not the shipping managed route.

Not tested: a styled dictation against the live writing service (the wording a real model produces for a style), the notch Style row with a real pointer on a physical PC, and a real microphone; fresh real browser sign-in, production-identity installation and monitor/DPI transitions. The installer is unsigned. No provider key or customer credential is embedded in these packages.
