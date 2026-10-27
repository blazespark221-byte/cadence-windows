# Cadence for Windows 1.2.38 — Agent models, live voice and connectors

- **Choose Cadence Agent's model.** The new Model button in the Agent composer, next to Manual / Full access, picks GPT-6 Luna (the default, on every plan) or Claude Opus 5.5 (Pro). Cleanup, Refine, Chat, Annotate and Translate are unchanged.
- **Talk with Cadence Agent live.** When you're signed in to your Cadence account, voice mode opens a live conversation: Cadence listens and answers while you talk, and hands what you ask for to the Agent, which does it with the same approvals as a typed request. Free includes 10 minutes a week and Pro 60, up to 10 minutes per conversation. Turn it off under Live voice in the Model menu. If live voice can't connect, Cadence uses the standard voice.
- **Connectors.** Cadence Agent can write emails: it opens a filled-in Gmail or email-app compose window for you to check and send. It never sends email itself. Add your own tools as MCP connectors in Settings → Connectors, with no sign-in, an API key or a browser sign-in; each tool asks before it runs unless you allow a connector's read-only tools. Gmail and Outlook sign-in, for saved drafts, isn't switched on in this version yet.
- **How many times faster than typing.** Home now says how many times faster than typing you are, compared with the average typing speed, in place of the Typing row and its adjustable speed.
- **Search every language in Translate.** The Translate card's language list has a search box: 108 languages by their English name, their own name (Español, 日本語) or another name (Farsi, Mandarin). Settings' "Translate into" lists them all too.
- **Update pop-up.** From this version on, when an update is out, Cadence shows an "Update available" window at launch, and Update now downloads, installs and restarts in one click.
- **Livelier level bars.** The dictation bubbles learn a quiet microphone's level, so they move when you speak even on a headset or a low input volume. Cadence Agent shows your microphone level with the same bars instead of a thin progress bar.
- Includes everything from 1.2.35.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
