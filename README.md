# T3 Status

A small floating desktop widget for **T3 Code + Claude** on Windows.

- Every chat T3 is running right now (and its subagents), with step progress.
- Amber when a chat is waiting for your answer or approval.
- Claude usage (5-hour and weekly) for **every Claude account** on your PC, found automatically.
- Context % of the chat open in T3.
- Tells you when there's a new version.

Native Windows app (Rust), about 2 MB, ~10 MB of memory.

## Install

Open **T3 Code**, start a new chat with **Claude**, and paste this:

```
Install or update the T3 Status widget on this PC from https://github.com/BliksemCode1/t3-status - follow INSTALL.md there.
```

Approve what it asks. That's the only time an AI is involved.

## Updates

When a new version is out, the widget shows a small blue dot. Right-click the tray icon (or click **⋯** on the
widget) → **Update to vX now**. It downloads the new version from this page's Releases, checks it against GitHub's
checksum, swaps it in and restarts. Press **↻** to check for a new version right away; otherwise it checks every hour.

## Using it

- **Ctrl+Alt+U** shows or hides it. Right-click the tray icon for the menu.
- Drag it anywhere; it snaps to screen edges and to the T3 window.
- Tray menu → **Stick to T3**: it follows the T3 window and hides when T3 is minimized (works with T3 maximized too).
- **▾** expands it, hover a row for details, click a task to open its chat in T3.

## Privacy

It only reads files on your own PC. It makes two kinds of internet calls: Anthropic (your own Claude usage,
with your own sign-in) and GitHub (is there a newer version?). Nothing about you or your PC is sent anywhere.

## Remove

Tray icon → untick *Start with Windows* → *Quit*. Then delete `%LOCALAPPDATA%\Programs\T3 Status` and
`%USERPROFILE%\.t3-status-widget`.

Needs Windows 10/11 and T3 Code desktop with Claude signed in.
