# Windows 1.2.9 release verification — 14 October 2026

Application source: 4ce2dcb146275b6cc91fb165f400c94084051c9e in blazespark221-byte/cadence (branch feature/notch-windows, on top of 1.2.8 19f13c3). The change is 5863960 (Cadence in the notch) and 4ce2dcb (mouse side-button shortcuts); 8fe814a sets the version and f8cdd19 merges the 1.2.8 release record.
Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/38564464333

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. Installer and portable ZIP hashes were checked against the build and artifact manifests after download.

What changed:
- Notch: a new Notch (top centre) floating-control position. It can be chosen in General settings or the panel's Position row, or by dropping the glass tab's handle near the top centre. Windows displays have no camera housing, so Cadence draws a 186 × 32 DIP black notch at the top centre of the docked display's work area. Hovering the notch or clicking it opens a black panel with the Mac notch controls. Hover is read from the pointer position, with a 100 ms entry delay and a 450 ms exit grace. The controls take clicks only once the panel has opened, and never activate Cadence. While docked, the dictation overlay becomes a Dynamic Island that grows out of the notch on the target window's display. Refine, the Cadence Agent request panel and its progress card hang from the notch on the docked display. Each surface animates with the Mac app's SwiftUI spring values inside a fixed transparent window. The notch hides while a full-screen app is in front on its display.
- Mouse side-button shortcuts: Mouse 4 or Mouse 5 can be the dictation, Refine or Cadence Agent shortcut. A WH_MOUSE_LL hook on its own message-loop thread runs only while a side button is assigned. It swallows the bound button's press and matching release, so the app under the cursor does not also go Back or Forward.

Executed on this candidate:
- 198 Windows logic/controller checks with zero failures (one separate desktop suite excluded). These include the new mouse side-button checks: validation, labels, reload, and press/release pairing.
- 41 portable Cadence Agent, streaming and settings parity checks. They include notch docking: the drop zone near the top centre, scaled displays, and the top-centre fallback.
- 47 packaged smoke checks on each of the portable, installed and upgraded copies, 8 of them for the notch. The dictation island hangs from the top centre and routes its Stop and recovery actions. The notch controls rest as the virtual notch and open with the Mac panel's actions. Refine and both Cadence Agent surfaces hang from the notch, and Refine keeps its panel size.
- 451 offscreen UI checks and 426 synthetic renders, including General's position choices with Notch (top centre).
- 12 native browser dictation checks with real Chrome and Edge on the runner desktop; 4 native opaque-editor checks; 6 native Cadence Agent checks against real Notepad.
- 283 managed-account checks; 7 packaged floating-control input checks; 16 managed .NET speech checks with local services; 62 managed-writing/core bridge checks.
- 16 package and lifecycle gates on the exact candidate: isolated upgrade from 1.0.4, restart/reinstall, settings and encrypted-session retention, uninstall, and updater commit/cancel/restart-failure handoffs.

Run on the development PC from this exact source, not on the runner:
- 7 native notch checks: the closed notch takes only its own click; hover opens the panel after its entry delay and the controls take clicks once it has opened; leaving gets its grace period, then the panel closes; an explicit open stays until the pointer has entered and left; dictation taking the notch closes the controls; choosing an edge brings back the glass tab; and the spring curves are checked.
- 177 logic checks, 4 modifier-registration checks, 7 floating-control interaction checks, 47 smoke checks, and the offscreen suite.

Real-screen captures at 100% scaling were taken during the notch change, before it was rebased onto 1.2.8. They show the notch opening and closing, the dictation island states, recovery, and Refine. The mouse side-button change's real-input Settings checks passed on the development PC before the final rebase; later runs lost foreground and were not repeated.

The optional legacy Swift bridge capability check failed its five-minute WAV boundary, as in 1.1.0 through 1.2.8. It is not the shipping managed route.

Not tested:
- hovering the notch with a real pointer on the runner (the checks drive the same hover entry point)
- the notch on a second display, above 100% scaling, with a top taskbar, or across monitor and DPI changes
- full-screen detection with real games and video players
- mouse side-button shortcuts from a physical mouse on the runner
- a physical microphone session
- real Google Docs (docs.google.com) on a Windows desktop
- the agent with the live AI service on Windows
- a real-user browser sign-in from the welcome guide
- production-identity installation

The installer is unsigned. No provider key or customer credential is embedded in these packages.
