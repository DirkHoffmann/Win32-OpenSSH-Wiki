OpenSSH follow the below rules to determine if the " and \ in shell arguments are escaped or not

|  DefaultShell | example to print out "hello" <br/>(client cmd run in cmd prompt)| Notes |
|--|--|--|
| powershell  | ``c:\>ssh.exe localhost echo `\"hello`\"``<br/>`c:\>"hello"` | PS strip the " |
|  bash | to be added | |
|  cygwin | to be added | | 
|  cmd.exe |  `c:\>ssh.exe localhost echo \"hello\"`<br/>`c:\>"hello"` | |
|  ssh-shellhost.exe | to be added | |
|  shells other than above | 1, not set | |
|  shells other than above | 0 | |

Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and DefaultShellEscapeArguments. 