# T3 Status

A small floating desktop widget for **T3 Code + Claude** on Windows.

- Every chat T3 is running right now (and its subagents), with step progress.
- Amber when a chat is waiting for your answer or approval.
- Claude usage (5-hour and weekly) for **every Claude account** on your PC, found automatically.
- Context % of the chat open in T3.
- Tells you when there's a new version.

Native Windows app (Rust), about 2 MB, ~10 MB of memory.

## Install or update

Open **T3 Code**, start a new chat with **Claude**, and paste this:

```
Install or update the T3 Status widget on this PC from https://github.com/BliksemCode1/t3-status - follow INSTALL.md there.
```

Approve what it asks. Use the same prompt to update. When an update is out, the widget shows **● UPDATE** and the
tray menu has an "Update available" item that copies this prompt for you.

## Using it

- **Ctrl+Alt+U** shows or hides it. Right-click the tray icon for the menu.
- Drag it anywhere; it snaps to screen edges and to the T3 window.
- **▾** expands it, hover a row for details, click a task to open its chat in T3.

## Privacy

It only reads files on your own PC. It makes two kinds of internet calls: Anthropic (your own Claude usage,
with your own sign-in) and GitHub (is there a newer version?). Nothing about you or your PC is sent anywhere.

## Remove

Tray icon → untick *Start with Windows* → *Quit*. Then delete `%LOCALAPPDATA%\Programs\T3 Status` and
`%USERPROFILE%\.t3-status-widget`.

Needs Windows 10/11 and T3 Code desktop with Claude signed in.
