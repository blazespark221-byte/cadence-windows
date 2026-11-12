# Windows 1.2.53 release verification - 12 November 2026

Application and package source: `ec395c1e56a710b0a70e65abfaba233fd80d29d9` in `blazespark221-byte/cadence`, branch `feature/redesign-windows`, based on Windows 1.2.52 (`041d3e76`). Build and acceptance: https://github.com/blazespark221-byte/cadence/actions/runs/43202819676 (attempt 1, source unmodified). Exact candidate stored in the private draft release `windows-candidate-1.2.53-43202819676`.

This release restyles the main window to the design the owner approved on 12 November 2026 (`c7a10bb7`). It changes only how existing features are laid out; no new behaviour is added:

- A 248 px sidebar: the brand mark and plan, a shortcut card whose dictation key cap is still the click-to-change button, pages in three groups (Speak: Today, Styles, Words; Write with AI: Refine, Chat; You: Your week, Settings), and a footer with the setup checklist (the welcome guide's three checks), the update control and this week's allowance meter.
- Today (the History page) is the launch page, with a one-sentence summary of today's usage counts and History's app names. Search, the app filter, Copy, Delete, the save-history-off state and the virtualized list are unchanged.
- Styles shows cards and the selected style below; Words (Dictionary) gains All / In use / Off filters and a Quick add rail that uses the editor's validation; Refine is a new page with a still picture of the review panel and the saved presets, each opening in Settings → Rewrite Presets; Your week (Home) shows four figures, a bar chart with today in red, the weekly allowance beside it and a "Where you spoke" bar computed from History.
- A new light and dark palette shared with Settings. Old page names still navigate: Home opens Your week, History opens Today, Dictionary opens Words, and Agent or Claude Code links open Today.

CadenceCore, the Swift bridge, the packaging tools and the installer are unchanged from 1.2.52. Both the shell and the bridge were still built fresh from clean source on an isolated Windows x64 runner. The downloaded ZIP and installer match the build's SHA-256 manifest. The bundled VERIFICATION.md is unchanged from 1.2.52 (same SHA-256).

Checks on this revision: 1889 managed-account checks; 120 portable parity checks. Windows application acceptance: 243 logic/controller checks (0 failures; 1 separate desktop suite skipped), 8 Annotate offscreen, 12 Chrome/Edge dictation, 5 opaque-editor, 13 native shortcut (including the sidebar key cap: click, press keys, Escape, a mouse side button and a refused Refine shortcut) and 10 clipboard checks. Exact-package checks: 4 headless gates (including the offscreen render suite, whose main-window checks were updated to the new titles, sidebar order, old-name navigation, Words filters, Styles selection, the Refine page and the allowance beside the chart), 7 floating-control checks and 16 isolated installer/lifecycle gates, including upgrade from 1.0.4, restart/reinstall, settings/encrypted-session retention, uninstall and updater handoffs.

Before the build, on the development PC: the offscreen suite passed 725 checks, the Chat offscreen suite 5, and each page was rendered off-screen in light and dark at 1440×900 and at the minimum window size (880×640) and compared with the design.

Remaining limits: the installer is unsigned. The new pages were checked off-screen and through UI Automation on the runner, not by a person on a physical display; production-identity installation, physical microphone dictation and real monitor/DPI transitions are not certified here. The optional legacy Swift speech capability result is false; it is separate from the shipping dictation path.

See verification-summary.json for exact machine-readable counts and flags.
