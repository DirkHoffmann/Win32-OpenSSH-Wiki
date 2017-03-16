## Build OpenSSH: (skip these steps if you’ve already done)
```powershell
Import-Module  .\openssh-portable\contrib\win32\openssh\appveyor.psm1 –Force
Start-SSHBuild -Configuration Debug -NativeHostArch x64 –Verbose
Install-OpenSSH -OpenSSHDir $env:SystemDrive\OpenSSH -Configuration Debug -NativeHostArch x64
```
## Run OpenSSH Pester Tests:
- Deploy OpenSSH tests
```powershell
Install-TestDependencies
Deploy-OpenSSHTests -OpenSSHTestDir $env:SystemDrive\OpenSSH -Configuration Debug -NativeHostArch x64
```
- Run pester tests : Launch powershell core windows (for example at **"$env:ProgramFiles\PowerShell\6.0.0.12\powershell.exe"**) and run the below command:
```powershell
cd $env:SystemDrive\OpenSSH
Run-OpenSSHPesterTest –testRoot $env:SystemDrive\OpenSSH -outputXml testresult.xml
```
   Note: If you want to run a particular test, skip step 3 and just launch it:
```powershell
.\SCP.Tests.ps1
```
