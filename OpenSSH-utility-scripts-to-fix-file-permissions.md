Powershell utility scripts are included starting release [V0.0.15.0](https://github.com/PowerShell/Win32-OpenSSH/releases/tag/v0.0.15.0) to automatically fix the permissions on various keys and configuration files for host and user. [Secure protection of various files](https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-Win32-OpenSSH) explains why secure enforcement is needed.
  - `FixHostFilePermissions.ps1`: checks and fixes the below permissions on default host files:
     - user's authorized_keys located at `$env:systemdrive\Users\...\.ssh\authorized_keys`
     - host keys generated by `ssh-keygen.exe -A` in the same folder of the script
     - sshd_config in the same folder of the script

```PowerShell
# script prompt to confirm you want to update each permission if Quiet is not specified
.\FixHostFilePermissions.ps1
```
  - `FixUserFilePermissions.ps1`: checks and fixes the below file permissions for user's default files: 
     - user's ssh_config located at `~\.ssh\config`
     - user's keys located at `~\.ssh\id_rsa`, `~\.ssh\id_rsa.pub`
     - user's keys located at `~\.ssh\id_dsa`, `~\.ssh\id_dsa.pub`

```PowerShell
# -Quiet suppresses prompting to confirm you want to update each permission
.\FixUserFilePermissions.ps1 -Quiet 
```
  - Powershell module `OpenSSHUtils.psm1` checks and fixes customer specified files.
    - Function `Fix-HostSSHDConfigPermissions` fixes the sshd_config file specified by user
    - Function `Fix-HostKeyPermissions` fixes the permission for host keys specified by user; **Note that to keep the host private keys secure, it is recommended to register them with ssh-agent following
steps in [link](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH). **, but this function make sure 'NT Service\sshd' Read permission to the host files for now in case they are not registered yet. 
    - Function `Fix-UserKeyPermissions` fixes the the permissions for user's key files specified by user
    - Function `Fix-AuthorizedKeyPermissions` fixes the permissions for the authorized_keys file specified by user
    - Function `Fix-UserSSHConfigPermissions` fixes the permissions for user's ssh config specified by user

```PowerShell
Import-Module .\OpenSSHUtils.psm1 -Force
# prompt to confirm you want to confirm you want to update each permission on the file
Fix-HostSSHDConfigPermissions c:\test\sshd_config
# -Quiet suppresses prompting to confirm you want to update each permission on the file
Fix-AuthorizedKeyPermissions -FilePath C:\Users\sshtest_ssouser\.ssh\authorized_keys -Quiet
Fix-HostKeyPermissions -FilePath c:\test\sshtest_hostkey_ecdsa -Quiet
Fix-HostUserPermissions -FilePath c:\test\sshtest_userssokey_ed25519 -Quiet
Fix-UserSSHConfigPermissions -FilePath '~\.ssh\config' -Quiet
```