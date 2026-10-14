# Cadence for Windows 1.2.7 — Alt shortcuts keep your place

- **Dictation with an Alt shortcut works every time:** with Left or Right Alt as the dictation shortcut, every other press stopped with “Couldn’t start recording · focus an accessible text field”, and finishing a dictation could leave the words waiting for Insert here. Pressing Alt on its own opens an app’s menu on Windows (in Chrome and Edge it moves focus to the ⋯ button), which pulled focus out of your text field. Cadence now keeps that Alt press from reaching the app, so focus stays where you’re typing.
- **Dictation into more desktop apps:** apps that draw their own editor, which Windows can’t identify as a text field, now receive dictation at the cursor, as on the Mac. Cadence still refuses buttons, menus, lists, links, password fields and read-only text.
- Includes Google Docs dictation in Chrome and Edge from 1.2.6, the weekly dictation allowance on Home from 1.2.5 and the Cadence Agent character from 1.2.4.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
