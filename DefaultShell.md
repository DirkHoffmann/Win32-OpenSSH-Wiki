If you configure a default shell, ensure that OpenSSH installation path is in system PATH. If not already present, amend system PATH and restart sshd service.

On the server side, configure the default ssh shell in the windows registry. 

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShell` - Full path (case sensitive) of the shell executable

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShellCommandOption` - The switch that the configured default shell requires to execute a command and immediately exit and return to the calling process. It is used for executing the remote ssh commands. _Example- ssh user@ip hostname_


***

> Example - Powershell cmdlets to set powershell bash as default shell
  
   * `New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force`


  * `New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShellCommandOption -Value "/c" -PropertyType String -Force`

***

If you are configuring the powershell.exe/cmd.exe/WSL-bash.exe as default ssh shell then you can ignore `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShellCommandOption`. Your registry should look like [this](https://user-images.githubusercontent.com/23668037/32013581-67206dca-b970-11e7-8820-fde658d302c1.png).

If you want to configure default shell (Ex- cygwin) other than powershell/cmd/WSL-bash then your registry should look like [this](https://user-images.githubusercontent.com/23668037/32015013-9e644cee-b974-11e7-8375-bf3d50f596df.png)