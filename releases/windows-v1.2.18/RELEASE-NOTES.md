# Cadence for Windows 1.2.18 — an account is required, and you can see which one

- **You need to sign in to use Cadence, including the free plan.** The welcome guide no longer lets you continue past "Your Cadence account", or choose "Set up later", until you're signed in. If you press a Cadence shortcut while signed out, Cadence offers **Sign in** instead of "Try again". Home leads with "Sign in to start using Cadence" until you do. The Cadence service already refused requests without an account; the app now says so up front.
- **Settings → Account shows who you're signed in as.** The top of the page reads "Signed in as" and your email, and the welcome guide shows the same line. Sign-ins saved by an earlier version show it after Cadence asks the service once.
- **Reinstalling keeps your sign-in.** Your sign-in is saved for your Windows account in `%LOCALAPPDATA%\Cadence`, which the installer leaves alone, so a reinstalled Cadence is still signed in. The welcome guide now says which account it found. Use **Sign out…** in Settings → Account to remove it.
- **Signing in ends back in Cadence, as on the Mac (from 1.2.17).** When your browser finishes signing you in, the welcome guide or Settings → Account comes back to the front. Before, Windows kept the browser in front, so it looked as if nothing had happened.
- **No more "Cadence for Mac wants to access Cadence" page (from 1.2.17).** That approval page came from the sign-in service, not from the app, and is turned off for the Cadence apps.
- Includes clearer usage messages from 1.2.17, the stuck-key shortcut fix from 1.2.16, dictation with a picture on your clipboard from 1.2.15, dictation at the cursor from 1.2.14 and Cadence in the notch by default from 1.2.13.

Includes the required .NET and Swift runtimes. The installer is unsigned. See RELEASE-VERIFICATION.md for the exact automated Windows checks and remaining limits.
