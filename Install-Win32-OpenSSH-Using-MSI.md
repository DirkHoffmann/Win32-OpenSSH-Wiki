# Prerequisites
1. Win32-OpenSSH Github releases can be installed on Windows 7 and up.
1. Note [these considerations](https://github.com/PowerShell/Win32-OpenSSH/wiki/Various-Considerations) and [project scope](https://github.com/PowerShell/Win32-OpenSSH/wiki/Project-Scope) first.
1. Download the [latest](https://github.com/PowerShell/Win32-OpenSSH/releases/latest) build of OpenSSH, selecting either the 32-bit or 64-bit MSI.

# Install Win32-OpenSSH using MSI
The MSI must be run in a command prompt, as it does not yet have a UI (coming soon). The commands to run, are as follows:
* To install both the SSH Client & the SSH Server (default behavior)  
`msiexec /i <path to openssh.msi>`
* To install only the SSH Client  
`msiexec /i <path to openssh.msi> REMOVE=Server`
* To install only the SSH Server  
`msiexec /i <path to openssh.msi> REMOVE=Client`

# Uninstall Win32-OpenSSH using MSI
Similarly, the command to uninstall Win32-OpenSSH is as follows:  
``msiexec /x <path to openssh.msi>``

# Additional Documentation on msiexec
Further information on msi command-line options can be found [here](https://docs.microsoft.com/en-us/windows/win32/msi/command-line-options)