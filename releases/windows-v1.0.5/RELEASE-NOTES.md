Windows 1.0.5 brings the current Mac features to Windows:

- One Cadence account for dictation and rewriting, with sign-in recovery, plan, remaining allowance, reset date and billing controls.
- None, Light and Medium dictation cleanup. Changes apply to the next recording; the raw transcript remains recoverable if cleanup fails.
- Update checks on Home, in the tray and in About, with download progress, cancellation and guarded restart/recovery.
- The same five-step setup order and everyday/More settings organization as the captured Mac version.
- Instrument Serif headings, refined light/dark UI, dictionary, presets, selection rewriting and caret composition.

Windows 10 build 19041+ on Intel/AMD x64. Required .NET and Swift runtimes are bundled. Use the setup installer or extract the entire portable ZIP. Sign in under **Settings → Account**. Fresh defaults are hold **Ctrl+Alt+Space** to dictate and **Ctrl+Alt+R** for Refine; upgrades preserve your choices.

This Windows release is unsigned. See **RELEASE-VERIFICATION.md** for exact test scope and remaining limits. Managed speech, native editor replacement/Undo, isolated 1.0.4 upgrades, settings/session retention and updater recovery passed. Fresh live browser sign-in, full live microphone workflows, monitor transitions and broader editor compatibility remain unverified. The optional legacy Swift speech protocol still timed out on its maximum upload; the shipping app uses the separately verified .NET speech transport.
