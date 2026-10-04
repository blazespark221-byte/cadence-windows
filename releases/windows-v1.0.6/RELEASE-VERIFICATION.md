# Cadence for Windows 1.0.6 - verification

Verified 5 October 2026 on Windows 11 x64 build 26200. Application source: `0b933496209e580c904ad4657fd89c4e07bbf248`, built from clean committed source. The Windows shell and Swift bridge were freshly packaged together with their runtimes. Frozen Core Contracts and Support are unchanged.

## Executed checks

- Windows Release build: zero warnings or errors.
- Windows logic: 154 passed; one desktop suite intentionally excluded from this logic-only invocation.
- Exact packaged UI: 404 checks and 384 offscreen renders passed. Checks exercise a manual update check, a release arriving in both open windows, navigation without losing the update action, minimum window sizes, and light/dark themes. Render scales are 100/150/200 percent, not native DPI certification.
- Artifact verifier: 512 payload files and five build-artifact hashes matched, including ZIP integrity and source/runtime provenance.
- Exact packaged managed speech: 16 passed, including five-minute upload and cancellation over Windows HTTP.
- Exact packaged Swift writing/core: 51 passed within the declared managed-app scope.
- Package lifecycle: 12 passed, zero failed. Portable and installed app launch without developer runtimes; isolated 1.0.5 to 1.0.6 upgrade; retained synthetic preferences/encrypted session bytes; reinstall, relaunch and owned uninstall. Tests use a distinct verification installer identity.
- Production Cadence files, registrations, shortcuts, settings and sessions remained unchanged by installer fixtures.
- Website: 60 tests passed, including Windows GET/HEAD download redirects. Deployment and live route evidence are recorded separately.

The first installer fixture attempt stopped at the harness's hardcoded 1.0.4 baseline assertion before installation. The harness now accepts the exact pinned released 1.0.5 source as well as 1.0.4. The rerun against the same candidate passed; no application code or package bytes changed during that repair.

## Limits

The optional legacy Swift speech protocol again timed out on the five-minute upload. This is retained as a separate failure; the shipping managed app uses the passing .NET speech transport. Writing and cleanup use the separately passing Swift bridge.

This patch changes update-control placement and preferences presentation. Native external-editor replacement/Undo and updater commit/cancel/rollback checks from 1.0.5 were not rerun and are historical coverage only. Fresh real browser sign-in, live microphone/service workflows, production-identity installation, updater handoff between distinct versions, native monitor transitions and broader editor compatibility remain unverified.

The installer is unsigned. Hashes establish byte identity, not publisher signing. Package VERIFICATION.md is a build-time note; this later record describes exact-candidate execution without altering the immutable installer or portable ZIP.
