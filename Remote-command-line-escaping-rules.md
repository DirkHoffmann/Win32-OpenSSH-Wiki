OpenSSH follow the below rules to determine if the " and \ in shell arguments are escaped or not

|  DefaultShell | DefaultShellEscapeArguments  |ShellPath is double quoted |" and \ are escaped in arguments|
|---|--|--|--|
| powershell  | value is ignored| yes | yes |
|  bash | value is ignored | Yes | Yes|
|  cygwin |  value is ignored | Yes | Yes |
|  cmd.exe |  value is ignored | Yes  | No |
|  ssh-shellhost.exe | value is ignored | Yes  | No |
|  Other custom shells | 1, not set | Yes  | Yes |
|  Other custom shells | 0 | Yes | No|

Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and DefaultShellEscapeArguments. 