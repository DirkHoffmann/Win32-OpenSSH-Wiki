# Prerequisites
1. Win32-OpenSSH Github releases can be installed on Windows 7 and up.
1. Note [these considerations](https://github.com/PowerShell/Win32-OpenSSH/wiki/Various-Considerations) and [project scope](https://github.com/PowerShell/Win32-OpenSSH/wiki/Project-Scope) first.
1. Download the [latest](https://github.com/PowerShell/Win32-OpenSSH/releases/latest) build of OpenSSH, selecting either the 32-bit or 64-bit MSI.

# Install Win32-OpenSSH using MSI
## 1. Run MSI Installer
The MSI must be run in any command prompt (cmd.exe & pwsh.exe both work), as it does not yet have a UI (coming soon).  
The MSI will install OpenSSH to the `ProgramFiles\OpenSSH` folder.  
The commands to run, are as follows:
* To install both the SSH Client & the SSH Server (default behavior)  
`msiexec /i <path to openssh.msi>`
* To install only the SSH Client  
`msiexec /i <path to openssh.msi> ADDLOCAL=Client`
* To install only the SSH Server  
`msiexec /i <path to openssh.msi> ADDLOCAL=Server`
* To uninstall only the SSH Client  
`msiexec /i <path to openssh.msi> REMOVE=Client`
* To uninstall only the SSH Server  
`msiexec /i <path to openssh.msi> REMOVE=Server`

###  Examples:
* Installing SSH Client & openssh.msi is in the working directory:  
`msiexec /i openssh.msi ADDLOCAL=Client`
* Installing SSH Server & openssh.msi is in C:\users\public\downloads\:  
`msiexec /i C:\users\public\downloads\openssh.msi ADDLOCAL=Server`
* Uninstalling SSH Client & openssh.msi is in the working directory:  
`msiexec /i openssh.msi REMOVE=Client`
* Uninstalling SSH Server & openssh.msi is in C:\users\public\downloads\:  
`msiexec /i C:\users\public\downloads\openssh.msi REMOVE=Server`

## 2. Update SYSTEM PATH (Required for SCP and SFTP)
Append the Win32-OpenSSH install directory to the system path, by running the following command in an elevated PowerShell session:  
`[Environment]::SetEnvironmentVariable("Path", [Environment]::GetEnvironmentVariable("Path",[System.EnvironmentVariableTarget]::Machine) + ';' + ${Env:ProgramFiles} + '\OpenSSH', [System.EnvironmentVariableTarget]::Machine)`

To verify that the System Path variable was modified properly, the Environment Variables can be viewed in Control Panel, under the Advanced tab. 
## 3. Verify OpenSSH Install
Check the status of the SSH Service.  
In PowerShell, run:   
`Get-Service -Name ssh*`

# Uninstall Win32-OpenSSH using MSI
Similarly, the command to uninstall Win32-OpenSSH is as follows:  
``msiexec /x <path to openssh.msi>``

# Additional Documentation on msiexec
Further information on msi command-line options can be found [here](https://docs.microsoft.com/en-us/windows/win32/msi/command-line-options)

# Video recording
https://user-images.githubusercontent.com/23668037/159090480-fb40882f-bf52-4dd7-a6b2-f3536128ab82.mp4