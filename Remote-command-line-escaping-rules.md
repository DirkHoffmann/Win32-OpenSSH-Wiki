
|  DefaultShell | DefaultShellEscapeArguments  |ShellPath is double quoted |" and \ are escaped in arguments|
|--|--|--|--|
| powershell  | 1, 0, missing | yes | yes |
|  bash | 1, 0, missing | Yes | Yes|
|  cygwin |  1, 0, missing | Yes | Yes |
|  cmd.exe |  1, 0, missing | Yes  | No |
|  ssh-shellhost.exe | 1, 0, missing | Yes  | No |
|  Other custom shells | 1, missing | Yes  | Yes |
|  Other custom shells | 0 | Yes | No|

Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and DefaultShellEscapeArguments. 