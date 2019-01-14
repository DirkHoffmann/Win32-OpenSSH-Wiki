OpenSSH follow the below rules to determine if the " and \ in shell arguments are escaped or not
Here are examples to print out "hello" on different shells

|  DefaultShell | cmd to print on local shell | cmd to print on remote shell (client cmd run in cmd prompt) |
|:--|:--|:--|
| powershell | ``echo `"hello`"`` |``c:\>ssh.exe winbox echo `\"hello`\"`` | 
|  bash | ``echo '"hello"'``<br/> or ``echo \"hello\"``| ``c:\>ssh winbox 'echo \"hello\"'``<br/> or `c:\>ssh.exe winbox echo \\\"hello\\\"` <br/> or `c:\>ssh winbox  echo '\"hello\"'`  |
|  cygwin | ``echo '"hello"'``<br/> or ``echo \"hello\"``| ``c:\>ssh winbox 'echo \"hello\"'``<br/> or `c:\>ssh.exe winbox echo \\\"hello\\\"` <br/> or `c:\>ssh winbox echo '\"hello\"'` | 
|  cmd.exe | `echo "hello"` |  `c:\>ssh.exe winbox echo \"hello\"`  |
|  ssh-shellhost.exe | to be added | to be added |

Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and DefaultShellEscapeArguments. 