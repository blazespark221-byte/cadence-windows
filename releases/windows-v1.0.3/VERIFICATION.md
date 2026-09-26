# Cadence 1.0.3 for Windows

Install **Cadence.exe**, then open Settings → General → Sign in to Cadence.
Your Cadence account connects dictation, spoken instructions, Refine and dictation cleanup.
New installations no longer ask you to configure personal providers or install Codex.
Required .NET and Swift runtimes are included. Windows 10 version 2004+ / Windows 11 x64.

Hold Ctrl+Alt+Space to dictate, release to insert. Select text and press Ctrl+Alt+R
for a rewrite, then review and apply. Existing shortcuts and local preferences are retained.
The account and plan button opens the Cadence website. Account limits and service availability apply.

## Verification of this exact package

- Source: 632136778c3455cbd5d861ada58c61d9e41a71c6; clean Windows CI build.
- 82 managed account checks and 4 independent recovery/race regressions passed.
- 110 Windows checks passed, zero failed; one desktop/hardware suite intentionally skipped.
- 299 offscreen UI checks and 294 renders passed; all prior required checks/render identities retained.
- Packaged app and bundled engine ran with installed-runtime/developer paths removed.
- Production installer fresh installation, reinstall, upgrade from the immutable public 1.0.2
  installer, protocol registration, settings preservation and uninstall passed on an isolated Windows runner.
- Microsoft Defender found no threats in the installer or expanded payload with signatures 1.459.410.0.
- Independent ZIP membership/CRC, 511 file hashes, engine provenance and artifact checksums passed.

The unchanged Swift engine retains its separately recorded 1.0.2 source provenance.
The new .NET shell is packaged as ordinary self-contained files without runtime self-extraction.
Upstream AI credentials stay on the server. Customer sessions use Windows DPAPI.

## Limits

The application and installer are **unsigned**. Defender scan results do not establish
SmartScreen reputation or guarantee that Windows will not show an unknown-publisher warning.
No named malware detection was provided for the earlier download, so no false-positive
submission or universally warning-free result is claimed.

Tests cover a real Windows callback pipe and registry registration, but not a customer's
interactive Google browser-to-app round trip. Microphone hardware and a full dictation-to-external-editor
workflow were not exercised on CI. Backend synthetic speech and writing requests separately passed.
The archive's build-time VERIFICATION.md defers to this post-build evidence.

This repository holds distribution documentation and verified binaries, not the private app source.
