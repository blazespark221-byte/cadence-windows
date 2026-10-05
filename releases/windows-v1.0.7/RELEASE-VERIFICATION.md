# Cadence for Windows 1.0.7 - verification

Verified 5 October 2026 on Windows 11 x64 build 26200. Application source: `863b1e53e45644d6e646873888681472841fe73d`, built from clean committed source. The Windows shell and Swift bridge were freshly packaged together with their runtimes. Frozen Core Contracts and Support are unchanged.

## Executed checks

- Windows Release build: zero warnings or errors.
- Windows logic: 156 passed; one desktop suite intentionally excluded from the logic-only invocation. New regressions cover missing/wrong installation registration and preserved failure messages, no premature restart, released restart leases and a successful retry after repair.
- Exact packaged UI: 404 checks and 384 offscreen renders passed, including update controls in both windows, navigation, minimum sizes and light/dark themes. Render scales are 100/150/200 percent, not native DPI certification.
- Artifact verifier: 512 payload files and five build-artifact hashes matched, including ZIP integrity and source/runtime provenance.
- Exact packaged managed speech: 16 passed, including five-minute upload and cancellation over Windows HTTP.
- Exact packaged Swift writing/core: 51 passed within the declared managed-app scope.
- Package lifecycle: 16 passed, zero failed. Portable and installed app launch with bundled runtimes; isolated 1.0.5 to 1.0.7 installation upgrade; synthetic preferences/encrypted session bytes retained; reinstall, relaunch and owned uninstall.
- Exact candidate updater helper: isolated same-version commit, cancellation and restart-failure rollback fixtures passed. Tests use a distinct verification installer identity and exercise the actual helper/installer/restart path.
- Production Cadence files, registrations, shortcuts, settings and sessions remained unchanged by the isolated fixtures.
- Website: 60 tests passed, including Windows GET/HEAD download redirects. Deployment and live-route evidence are recorded separately.

## Reported failure and one-time repair

The affected 1.0.5 copy had no Windows uninstall registration, although its installed files matched the released build. The updater rejected that copy before launching its helper, and the interface obscured that specific error with a generic restart notice. No cause for the missing registration has been established.

With Cadence fully quit, the original SHA-256-verified 1.0.5 setup was rerun. It restored the Windows registration, returned success and preserved the exact settings and encrypted session bytes. Cadence remained closed on 1.0.5 for the user's manual in-app upgrade. Version 1.0.7 makes future startup failures visible and gives the specific repair steps; it does not silently repair registration itself.

## Limits

The optional legacy Swift speech protocol again failed the five-minute upload check. This separate failure is not counted as a managed-app pass: shipping Windows speech uses the passing .NET transport. Writing and cleanup use the separately passing Swift bridge.

The user's normal in-app upgrade from 1.0.5 to 1.0.7 has not yet been verified. The automated installation upgrade crosses versions; updater-helper commit/cancel/rollback fixtures use the same version. Native external-editor replacement/Undo coverage is historical from 1.0.5. Fresh browser sign-in, live microphone/service workflows, the 1.0.7 production-identity installation, native monitor transitions and broader editor compatibility remain unverified.

The installer is unsigned. Hashes establish byte identity, not publisher signing. Package VERIFICATION.md is a build-time note; this later record describes exact-candidate execution without altering the immutable installer or portable ZIP.
