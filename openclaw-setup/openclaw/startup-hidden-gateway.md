# Hidden OpenClaw Gateway Startup

Current state as of 2026-07-04 KST:

- Windows scheduled task: `OpenClaw Gateway`
- Task state: `Running`
- Execute: `C:\Windows\System32\wscript.exe`
- Arguments: `"%USERPROFILE%\.openclaw\gateway.vbs"`
- Hidden: `True`
- Gateway process listens on: `127.0.0.1:18789`

## Launcher

`%USERPROFILE%\.openclaw\gateway.vbs`

```vbscript
' OpenClaw Gateway launcher.
' ASCII-only launcher avoids Windows Script Host mojibake in non-ASCII user paths.
Set shell = CreateObject("WScript.Shell")
scriptPath = shell.ExpandEnvironmentStrings("%USERPROFILE%") & "\.openclaw\gateway.cmd"
shell.Run """" & scriptPath & """", 0, True
```

`0` hides the window. `True` keeps the scheduled task in `Running` state while the gateway is alive.

## Verification

```powershell
Get-ScheduledTask -TaskName 'OpenClaw Gateway' |
  Select-Object TaskName,State,
    @{Name='Execute';Expression={$_.Actions.Execute}},
    @{Name='Arguments';Expression={$_.Actions.Arguments}},
    @{Name='Hidden';Expression={$_.Settings.Hidden}}

Get-NetTCPConnection -LocalPort 18789 -State Listen

Invoke-WebRequest -UseBasicParsing -Uri 'http://127.0.0.1:18789/' -TimeoutSec 5
```

