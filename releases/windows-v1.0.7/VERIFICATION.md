# Cadence 1.0.7 for Windows

This patch preserves and displays restart failures after update confirmation, including actionable guidance for missing Windows installation registration. It retains the bottom-left update controls. It retains the Windows 1.0.5 feature set: Cadence account sign-in, account usage and billing, None/Light/Medium dictation cleanup, update checks, five-step account-first setup, and the reorganized settings. Customers do not supply provider keys. Both the Windows shell and Swift bridge are built from the same source revision recorded in `build-manifest.json`. Matching Swift and multi-file .NET Desktop runtimes are included; the package does not reuse the Windows 1.0.2 engine or extract a .NET single-file bundle at startup.

The manifest records source cleanliness, source fingerprints, runtime versions and each payload file's hash. `SHA256SUMS.txt` identifies the exact installer, portable ZIP, manifest and these notes. A local diagnostic build explicitly marked as modified source must not be published as a verified release.

Build success and offscreen rendering do not establish complete acceptance. Check the candidate's separate reports for code/unit checks, loopback bridge requests, native editor workflows, microphone hardware, synthetic-audio live-service results, sign-in, installer upgrade/restart and updater behavior. Missing, blocked or failed checks remain open; no build-time note converts them into passed checks.

Managed Windows speech uses the packaged .NET transport; writing/cleanup use the packaged Swift bridge. Consult RELEASE-VERIFICATION.md for checks executed on this exact release. The prior 1.0.5 release passed packaged .NET speech and managed Swift writing checks, but its optional legacy Swift speech path timed out on a five-minute upload. Historical checks are not counted as fresh acceptance for this patch.

This candidate is unsigned unless its actual signature verification says otherwise. A hash match detects changed bytes but is not a substitute for a trusted publisher signature. No Windows security setting is disabled by Cadence or the verification scripts.

Requires Windows 10 build 19041 or later on Intel/AMD x64. Windows 11 x64 is the development acceptance host; other OS versions, ARM emulation and individual third-party editors need their own compatibility evidence. Settings and DPAPI-encrypted customer sessions are retained across installation and uninstall. Never upload ambient microphone audio for automated acceptance; live speech checks use synthetic speech only.

The Mac reference is the byte-recorded 1 October 2026 snapshot in the source repository. Native Windows controls, notification-area integration and Windows shortcut bindings adapt the Mac experience to Windows. Native monitor transitions, a fresh real browser sign-in and broader editor coverage are not certified by this release. See the release's final RELEASE-VERIFICATION.md for executed checks on the exact delivered bytes.
