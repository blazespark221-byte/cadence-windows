# Cadence for Windows 1.0.2 RC1 — verification notes

**Unsigned prerelease.** This is a tested candidate, not a certified stable release. Windows may display an unknown-publisher/SmartScreen warning. No signing or notarization claim is made.

## Downloads and requirements

- Windows 10 version 2004/build 19041 or later; tested on Windows 11 x64 build 26200.
- Intel/AMD x86-64 CPU. No native ARM64 or 32-bit build; ARM emulation is unverified.
- Required .NET, Swift and matching runtime components are bundled. End users do not need a developer SDK.
- Installer uses the current user's account without elevation. For portable use, extract the entire ZIP and keep the engine folder beside Cadence.exe.
- A microphone is required for voice input. Personal speech/text provider configuration and network access to that provider are required unless using a compatible local service.

| File | Bytes | SHA-256 |
| --- | ---: | --- |
| Cadence-1.0.2-windows-x64-setup.exe | 67460978 | `d0eb2cb38f7e57f71392c26d6b690f7f919e392a0bc12882cfeeb195ca4f14f7` |
| Cadence-1.0.2-windows-x64-portable.zip | 96696457 | `78ab7dd846b2787e06f70936ca9adeabb23b780dc0cb4d606abf9a08d1186a2f` |

SHA256SUMS.txt covers the executable, archive and accompanying verification/provenance files. The exact Cadence.exe inside the archive is 163061191 bytes, SHA-256 `f43528381923bc23aeed802a7de68ab39ae06a2313d8a6cbecd7229e8ec16b8e`. All 49 payload hashes/sizes and ZIP CRC were checked.

## Fresh-install shortcuts

- **Ctrl+Alt+Space:** hold to record dictation; release to stop, transcribe and insert.
- **Ctrl+Alt+R:** select text first, then press to open Refine and record your spoken instruction; press again to stop recording. Review the generated rewrite before accepting replacement.
- **Escape:** cancel the current operation.
- Both shortcuts and hold/toggle modes can be changed in Settings → Shortcuts. Right Ctrl is an optional modifier-only binding, not the fresh-install default. Upgrades preserve previously saved bindings/modes; older settings may retain toggle dictation.
- You may type instructions in Refine instead of recording them. Generation and insertion still depend on the configured writing provider and a valid target.

## Providers and accounts

**Managed Cadence accounts, billing entitlements and hosted speech are not implemented in this Windows build.** Users must configure their own speech and writing providers, using personal API keys or compatible endpoints/local services. Writing also supports the separately installed official Codex client signed in with ChatGPT. Codex sign-in does not supply speech transcription or a Cadence managed account. Provider charges, if any, are separate. No credentials are bundled.

## Checks completed on 16 September 2026

| Verification | Result |
| --- | --- |
| Windows Release build | 0 warnings/errors |
| Isolated logic/controller | 107 passed, 0 failed, 1 desktop-suite skip |
| Exact packaged executable offscreen controls | 299 passed, 294 renders |
| Headless package checks | 3 passed |
| Bundled provider bridge | 25 passed |
| Current package/install/upgrade/uninstall lifecycle | 8 passed |
| Portable/installed/upgraded visible smoke | 39 checks and 32 renders each; measured 144 DPI |
| Native tray target retention/refusal | 3 passed |
| Native Refine controller/bridge/review/replace | 1 passed, Undo retained |
| Native shortcut capture Tab/Shift+Tab/Escape | 3 passed |

Self-contained startup was checked after removing developer/runtime paths, pointing DOTNET_ROOT at a nonexistent directory and disabling multilevel lookup. Visible smoke used real packaged windows and isolated test settings.

Installer lifecycle used the identical payload and production installer recipe under a separate verification AppId, mutex, shortcut group and destination. The distributed production-identity installer was not itself executed. Existing production Cadence registrations and shortcuts remained unchanged.

Native Refine used the actual controller and bundled bridge with a synthetic loopback writing provider, review and exact selected-range replacement in an owned native editor. This pass used direct native insertion with no clipboard access or microphone/audio. The strengthened tray lane passed selection retention and changed-selection/child refusal; an earlier fixture discrepancy did not recur. No runtime guard was weakened.

The original attached icon is preserved byte-for-byte; the Windows ICO derives from it. Native captures verify light/dark chrome, tray presentation and Refine recovery using synthetic preview state. Complete independent Mac/Windows equivalence, all monitor transitions and notification-area positioning are not certified.

## Remaining limitations

- **Live microphone/provider end-to-end testing is incomplete.** This final pass opened no microphone and played no sound. The complete recording → live speech provider → paste/cancellation flow was not exercised.
- No personal Windows speech configuration was present on the test host. No credentials were copied or provisioned. A synthetic loopback response is not proof of live speech accuracy or latency.
- The extended clipboard suite refused unsupported existing image/app-owned formats; user clipboard data were not cleared to force a pass.
- Ordinary personal onboarding/live connections, other Windows versions, native ARM64, monitor transitions, sleep/resume and long sessions remain unverified.
- Earlier native baseline and local microphone checks exist, but are not presented as complete current-build live acceptance.
- The embedded VERIFICATION.md in the unchanged binary package reflects its earlier build-time checkpoint. These version-specific published notes supersede it for later verification results.

## Source and distribution provenance

Application binary source: `blazespark221-byte/cadence@1f536935b37b5a2bc758ac05e4274fd4234e0792`, clean build (`sourceModified: false`). Verification tooling/evidence revision: `50e90002bb8d2d9a7ad4778ba4ae894817ab8ec3`.

The [application source tag](https://github.com/blazespark221-byte/cadence/tree/windows-v1.0.2-rc.1) points to the exact binary source. That repository is private and requires authorized access; this release does not make its source public.

The public [distribution tag](https://github.com/blazespark221-byte/cadence-windows/tree/windows-v1.0.2-rc.1) points to a dedicated distribution documentation/provenance commit, not to unrelated application code. Its release-provenance.json and build-manifest.json identify the binary source explicitly. Existing Windows 1.0.0 RC1 assets are preserved.

GitHub release immutability locks this prerelease's assets and distribution tag after publication. It does not code-sign the executable, certify stable acceptance, or make the private application source public.
