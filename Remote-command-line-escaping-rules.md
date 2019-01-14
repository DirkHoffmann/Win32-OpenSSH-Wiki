OpenSSH follow the below rules to determine if the " and \ in shell arguments are escaped or not

|  DefaultShell | DefaultShellEscapeArguments |Example to print out "hello" <br/>(client cmd run in cmd prompt)| Notes |
|:--|:--|:--|:--|
| powershell  | N/A | ``c:\>ssh.exe localhost echo `\"hello`\"`` | PS strip the " |
|  bash | N/A | to be added | |
|  cygwin | N/A | to be added | | 
|  cmd.exe | N/A |  `c:\>ssh.exe localhost echo \"hello\"` | |
|  ssh-shellhost.exe | N/A | to be added | |
|  shells other than above | 1, not set | | |
|  shells other than above | 0 | | |

Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and DefaultShellEscapeArguments. 