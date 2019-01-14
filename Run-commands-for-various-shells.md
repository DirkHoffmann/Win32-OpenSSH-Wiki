Here are examples to run commands on remote shell over openssh. Examples are to print out "hello" remotely.

|  DefaultShell | cmd on local shell | cmd to print on remote shell (client cmd run in cmd prompt) |
|:--|:--|:--|
| powershell | echo `'"hello"'`<br/> or ``echo `"hello`"`` |`c:\>ssh.exe localhost echo '\"hello\"'` <br/> or ``c:\>ssh.exe winbox echo `\"hello`\"``<br> or ``c:\>ssh.exe localhost "echo `""hello`"""`` | 
|  bash | ``echo \"hello\"``<br/> or ``echo '"hello"'``| ``c:\>ssh winbox 'echo \"hello\"'``<br/> or `c:\>ssh.exe winbox echo \\\"hello\\\"` <br/> or `c:\>ssh winbox  echo '\"hello\"'`  |
|  cygwin | ``echo \"hello\"``<br/> or ``echo '"hello"'`` | ``c:\>ssh winbox 'echo \"hello\"'``<br/> or `c:\>ssh.exe winbox echo \\\"hello\\\"` <br/> or `c:\>ssh winbox echo '\"hello\"'` | 
|  cmd.exe | `echo "hello"` |  `c:\>ssh.exe winbox echo \"hello\"`<br/> or `c:\>ssh.exe winbox "echo ""hello"""`  |
|  ssh-shellhost.exe | to be added | to be added |

If you have a shell other than above and want it to receive exactly the same argument list that the ssh received on the server side, Please refer to [DefaultShell](https://github.com/PowerShell/Win32-OpenSSH/wiki/DefaultShell) for setting DefaultShell and set DefaultShellEscapeArguments to 0.