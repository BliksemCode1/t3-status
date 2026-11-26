# T3 Status: install / update steps (for the agent)

You are a Claude agent running in T3 Code on the user's Windows PC. Install or update the T3 Status desktop widget.
Use PowerShell. Do every step, then report back. Don't change anything else on the PC.

## 1. Install or update the program

```powershell
$dir = Join-Path $env:LOCALAPPDATA 'Programs\T3 Status'
$exe = Join-Path $dir 't3-status.exe'
$tmp = Join-Path $env:TEMP 't3-status-download.exe'
Invoke-WebRequest 'https://github.com/BliksemCode1/t3-status/releases/latest/download/t3-status.exe' -OutFile $tmp -UseBasicParsing
Get-Process t3-status -ErrorAction SilentlyContinue | Stop-Process -Force
Start-Sleep -Seconds 1
New-Item -ItemType Directory -Force $dir | Out-Null
Move-Item -Force $tmp $exe
Unblock-File $exe
New-ItemProperty -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Run' -Name 'T3 Status' -Value "`"$exe`"" -PropertyType String -Force | Out-Null
Start-Process $exe
```

Check the download is a real program (more than 1 MB) before replacing the old one. The widget appears as a
small floating bar and a tray icon. Settings and layout (`%USERPROFILE%\.t3-status-widget`) are kept on update.

## 2. Teach the user's Claude agents to report progress

This makes every chat, in every project, show its steps in the widget. Find every Claude config folder:

- `%USERPROFILE%\.claude`
- every other `%USERPROFILE%\.claude-*` folder
- every Claude provider in T3's `%USERPROFILE%\.t3\userdata\settings.json` (`providerInstances` entries whose
  `driver` contains "claude"; the folder is `config.homePath`)

In each folder, open `CLAUDE.md` (create it if missing). If it does **not** already contain the heading
`## Busy status (T3 Status widget)`, **append** the block below to the end. Never delete or rewrite anything already
in the file. On an update, leave an existing block alone.

````markdown
## Busy status (T3 Status widget)

For every task you work on, however small (even a single step or a quick question that needs tool use),
keep `<project root>/.claude/status.json` up to date so I can follow progress in the T3 Status widget
(floating bar on my desktop):

```json
{"task":"Short task name","steps":["Step one","Step two","Step three"],"done":1,"thread":"<value of $T3CODE_THREAD_ID>"}
```

- Write it as soon as you start working on a message (also when the previous task in this chat was marked Idle),
  and bump `done` after each step. A one-step task is fine: `"steps":["What you are doing"]`.
- In T3 Code, set `thread` to the `T3CODE_THREAD_ID` environment variable, so clicking the task in the widget
  opens this chat. Leave it out when that variable isn't set.
- When finished, set `"task":"Idle: <what was done>"` with `"steps":[]`.
- Write the file with plain UTF-8 (no BOM).
- Make sure `.claude/status.json` is in the project's `.gitignore` (when the project is a git repo).
````

## 3. Check it works

- Confirm the `t3-status` process runs from `%LOCALAPPDATA%\Programs\T3 Status\t3-status.exe` and the Run
  registry value points at it.
- Write `.claude/status.json` in this chat's project now (task "Setting up T3 Status", your steps, `thread` =
  `$env:T3CODE_THREAD_ID`) so this chat shows up in the widget.
- Take a screenshot of the whole virtual screen (PowerShell `System.Drawing` `CopyFromScreen`; call
  `SetProcessDPIAware` first) and look at it: the widget should show this chat as a task and a usage row per Claude
  account. If a row says "sign in", tell the user which account.
- Set the status file to Idle when done.

## 4. Report

In a few short lines: installed or updated, which `CLAUDE.md` files got the rule (or already had it), and:

- Right-click the tray icon for the menu; **Ctrl+Alt+U** shows or hides the widget.
- Drag it anywhere; it snaps to screen edges and the T3 window. **▾** expands, hover for details, click a task to
  open its chat.
- The rule only applies to chats started from now on.

No plugins, extensions, MCP servers or skills are needed.
