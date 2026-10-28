# Cadence for Windows 1.2.41: background Agent

- Open Cadence Agent and enable **Work in background** for typed or spoken requests, including tasks delegated by live voice.
- Run noninteractive PowerShell commands without opening a terminal window. Cadence reads the exit code and output; Stop cancels the owned process tree. Each command has a 120-second maximum.
- Read an existing app window and use supported controls without switching windows, moving the pointer, sending global keys or changing the clipboard. Unsupported controls return an explanation. An app's own button can still open UI.
- Manual mode asks before commands and control changes. Command output and the selected window's readable text go to your configured writing provider. Background mode omits connector tools that open windows.
- Includes all features from 1.2.40, including on-device Parakeet dictation.

Try: **Run Get-Location in the background and tell me the result.**

Includes the required runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for exact checks and remaining limits.
