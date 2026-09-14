# Windows release verification

Verification date: 14 September 2026. Host: Windows 11 x64, build 26200.

The Windows application is a native .NET 8 WPF tray host using the existing Swift
CadenceCore provider implementations through a private JSON-lines helper. The app
bundles its .NET Desktop, Swift, and required app-local runtime libraries. Existing
macOS contracts and services were not changed by the Windows port.

## Executed checks

| Area | Evidence | Result |
| --- | --- | --- |
| Shared Swift core | `tools/windows/all.ps1`, local mock provider server | 518 checks passed in 14 suites; zero failures |
| Swift Windows bridge | `Sources/CadenceWindowsBridge/Tests/bridge.test.mjs` | 39 checks passed |
| Independent bridge integration | `tools/windows/bridge-integration-tests.js` | 23 checks passed against private local HTTP fixtures |
| Official Codex client | Integration harness with `--codex` | Additional real synthetic rewrite passed; helper EOF terminated its Codex child |
| Windows settings, credentials, controller and target anchors | `windows/Cadence.Windows.Checks`, `--offline` | 38 checks passed; zero failures, one native lane explicitly skipped |
| Reference design and UI behavior | Actual WPF window rendering and control interaction | 28 checks passed; eight pop-up states and eight application/review screens captured |
| Native resources | Initial native harness run | Global shortcut conflict/release, clipboard Unicode/HTML restoration and concurrent change protection, three actual microphone capture cycles passed |
| Distribution | `tools/windows/verify-package.js --install` | Seven package checks; final rebuild verification recorded alongside artifacts |

Windows checks include real UI Automation against WPF and native EDIT controls:
unchanged selections, moved carets, identical text at another occurrence, changes to
the document, read-only rejection, and exact Unicode/multiline replacement confirmation.
Own-control edits are programmatic and do not count as external-application paste tests.
Settings regressions suspend the actual persistence semaphore after encrypted keys change,
then verify operation gating and correct endpoint/credential pairing after success and
rollback. An uncertain insertion stays blocked after regeneration.

Bridge integration includes Unicode, both speech adapters, all three HTTP text
protocols, model discovery, connection tests, response refusals/truncation/malformed
data, request cancellation, concurrent requests, JSON framing recovery, invalid audio,
remote cleartext rejection, and cross-origin redirect rejection. The production
helper is used; fixtures do not replace its provider implementation.

The package verifier removes developer and Swift paths, points `DOTNET_ROOT` to a
nonexistent directory, launches the actual self-contained app, exercises the packaged
Swift engine, verifies every manifest hash, installs to a disposable per-user location,
starts the installed app, upgrades it in place, and uninstalls it. These checks establish
bundling on the tested host; they are not a substitute for a clean Windows VM matrix.

## Interactive verification limit

Final external-editor insertion and password-field checks require an active test
window. An invisible Windows Search surface held foreground ownership on this host,
and the native UI automation could not activate the disposable test editor. The
harness now checks exact foreground ownership before any application input and
aborts if it cannot obtain it. The final native lane recorded 38 passing component
checks and one failing harness gate: "The test editor could not become active; no
application input was sent." No successful insertion claim is made from that run.

Run the native lane on an unlocked desktop and bring **Cadence native verification**
to the foreground. It covers selected Unicode capture, selection-only replacement,
changed-selection refusal, cancelled insertion, password-field refusal, clipboard
preservation, shortcut lifecycle, and microphone lifecycle:

```powershell
dotnet run --project windows/Cadence.Windows.Checks -c Release -- --native --report tools/windows/out/windows-native-checks.json
```

Provider credentials are not bundled. Real paid OpenAI/Anthropic endpoints were not
tested with end-user keys; their adapters were tested against local protocol fixtures.
The real configured official Codex client was exercised with synthetic text. Actual
speech accuracy requires a configured speech service and spoken test audio.

Windows 10, other Windows 11 builds, ARM emulation, per-application accessibility,
multi-monitor DPI changes, sleep/resume, and long-duration soak testing remain separate
verification work. Password fields and elevated applications are intentionally refused.

## Reference design

The user's **Cadence Dictation Pop-up.html** supplies the visual design. Its original
1254 × 1254 PNG is embedded unchanged in the Windows resources; a multi-resolution ICO
is generated from those pixels for the executable, tray, installer and shortcuts.
The source PNG SHA-256 is:

`63f518cfc403819b48877bca19b5ff40539e4e589cceaac1a103bf1a14e7fd4d`

The native pop-up follows the source's black 40-DIP pill, 20-DIP radius, five white
waveform bars, gray tabular timer, 24-DIP cancel button, status glyphs, error/recovery
cards, copy confirmation and raw-transcript recovery. It uses live microphone levels,
actual operation states and target-checked actions. Windows motion preferences are
respected. Settings and rewrite surfaces use the same neutral palette and original logo.

WPF smoke tests capture actual rendered application windows and all pop-up states.
Reference inspection uses the supplied HTML/CSS and extracted image; browser policy
blocked direct local HTML capture, so no browser-to-native pixel-diff score is claimed.
Native font rasterization and Windows taskbar placement differ from the web/macOS host.

## Reproduce and package

```powershell
node tools/mock-providers/server.js --port 18765 --quiet
# In another shell:
./tools/windows/all.ps1 -MockBase http://127.0.0.1:18765
swift build --product CadenceWindowsBridge -c release --scratch-path .build/windows-bridge
node Sources/CadenceWindowsBridge/Tests/bridge.test.mjs
node tools/windows/bridge-integration-tests.js --engine .build/windows-bridge/x86_64-unknown-windows-msvc/release/CadenceWindowsBridge.exe
dotnet run --project windows/Cadence.Windows.Checks -c Release -- --offline --report tools/windows/out/windows-controller-checks.json
./tools/windows/package-app.ps1
node tools/windows/verify-package.js --install
```

Reports and screenshots are written under `tools/windows/out`; distributable artifacts,
the file manifest and `SHA256SUMS.txt` are under `dist/windows`. Packaging accepts
`-DotNet` and `-InnoCompiler` when the toolchains are installed in a workspace directory.

No publicly trusted Windows code-signing identity was available. The artifacts are
unsigned and may display an unknown-publisher/reputation prompt. Do not label the build
as having passed complete end-user compatibility verification while the interactive
gate and operating-system matrix above remain outstanding.
