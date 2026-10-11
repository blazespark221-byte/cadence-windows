# Windows 1.1.1 release verification — 11 October 2026

Application source: 8c8b8034ae98a81fff3728f68043604fccb79660 in blazespark221-byte/cadence.
Build and acceptance workflow: https://github.com/blazespark221-byte/cadence/actions/runs/38141240404

The Windows shell and Swift bridge were built fresh from clean source on an isolated Windows x64 runner. All 512 payload file hashes and the exact installer/portable artifact hashes were independently checked after download.

Executed checks:
- 177 Windows logic/controller checks, zero failures; one separate desktop suite was excluded.
- 283 managed-account and 37 portable streaming, Assistant and settings checks passed in CI.
- 418 offscreen UI checks and 396 synthetic renders, including all seven accessible daily totals, exact point selection, populated/empty graphs and light/dark fixtures. Some fixed-height standalone chart captures clip the lower labels; the full Home capture shows the dates, with remaining content reachable by the existing scroll view.
- 7 checks against the packaged floating-controls DLL.
- 57 managed-writing/core bridge checks and 16 managed .NET speech checks using local test services.
- 4 headless package gates and 16 isolated installation/update lifecycle gates.
- Isolated upgrade from 1.0.4, restart, settings/encrypted-session retention, uninstall, and updater commit/cancel/restart-failure rollback passed.

The installer remains unsigned. Production-identity installation, fresh customer Google/email sign-in, physical microphone/live provider sessions, external-editor insertion, monitor transitions and broad OS coverage were not newly tested. Installer fixtures use isolated identities and temporary data; synthetic renders do not certify real monitor DPI transitions.

The optional legacy Swift speech path still fails its five-minute upload check, as in 1.1.0. It is not the shipping managed speech route. Current managed speech and streaming were checked with local HTTP/WebSocket fixtures, not a customer service session.
