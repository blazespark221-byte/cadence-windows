# Cadence 1.0.4 for Windows

Install Cadence.exe, sign in to Cadence, and allow microphone access.
Dictation and Writing are both shown as Default. Your account includes both models,
spoken instructions, Refine and optional cleanup. Required runtimes are included.
Windows 10 version 2004+ and Windows 11 x64 are supported targets.

This release replaces technical connection failures with Cadence recovery instructions
and shows the actual installed version in Diagnostics. Existing shortcuts and preferences
are preserved. Hold Ctrl+Alt+Space to dictate; select text and use Ctrl+Alt+R for Refine.
Account limits and service availability apply.

## Verification of this exact package

- Source: 0f5baa0090d7b549f09a12c8dc2b623aea55299a; clean Windows CI build.
- 182 managed account/recovery checks and four account regressions passed.
- 110 Windows logic/controller checks passed; zero failed, one hardware suite skipped.
- 309 packaged offscreen checks and 294 renders passed. General was visually inspected.
- Three exact-package runtime checks and ten installer/scan checks passed.
- Fresh install, reinstall, upgrade from public 1.0.2, settings preservation,
  callback registration, and uninstall passed on an isolated Windows runner.
- Microsoft Defender found no threats using signatures 1.459.455.0.
- Installer/ZIP checksums, ZIP membership/CRC, all 511 payload-file hashes and
  all 34 unchanged engine files were independently verified after download.

CI: https://github.com/blazespark221-byte/cadence/actions/runs/36531396922

The unchanged Swift engine retains its separately recorded 1.0.2 source provenance.
Shared AI credentials remain on Cadence's server. Customer sessions use Windows DPAPI.

## Limits

The application and installer are unsigned. Windows may show an unknown-publisher
or reputation warning; Defender results do not establish signing or SmartScreen trust.
Customer browser sign-in, microphone hardware and full dictation into external editors
were not exercised in this run. Synthetic checks do not establish complete hardware
or feature parity with Mac. Service health and sign-in configuration were checked;
this release run did not make live inference requests or alter customer accounts.

This repository contains distribution documentation and verified binaries, not private app source.
