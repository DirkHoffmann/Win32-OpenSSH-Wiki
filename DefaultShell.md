To configure a default shell, ensure that the following prerequisites are met
 - OpenSSH installation path is in system PATH. 
   - If not already present, amend system PATH and restart sshd service.

Follow these steps:
- On the server side, configure the default ssh shell in the windows registry. 
  - `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShell` - full path of the shell executable
  - `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH\DefaultShellCommandOption` (optional) - switch that the configured default shell requires to execute a command, immediately exit and return to the calling process. By default this is `-c`. 

***

> Powershell cmdlets to set powershell bash as default shell
  
   * `New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force`


  * `New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShellCommandOption -Value "/c" -PropertyType String -Force`

***

Example -
If you are configuring the powershell.exe/cmd.exe/WSL-bash.exe as default ssh shell, your registry should look like [this](https://user-images.githubusercontent.com/23668037/32013581-67206dca-b970-11e7-8820-fde658d302c1.png).
