Various OpenSSH resource files are integral to secure working of both server and client stacks. Here we discuss how to protect these resources, how OpenSSH for Windows enforces permission checks and individual case studies on how to fix any permission related issues. 

Improper file permissions will likely result in a broken configuration (OpenSSH fails to work). Here, you'll find icacls based commands to fix such issues.

2 fundamental reasons leading to the differences between how these permission checks work on Unix vs Windows:
- SuperUser on Unix maps to either [System (SY)](https://msdn.microsoft.com/en-us/library/windows/desktop/ms684190(v=vs.85).aspx) or AdministratorsGroup (AG) on Windows. 
- Permission controlling in Windows is more granular than in Unix. 


Its important to understand the distinction between "AdministratorsGroup" and an admin user. A logged on admin user would typically run processes in [non-elevated](https://msdn.microsoft.com/en-us/library/windows/desktop/dn742497(v=vs.85).aspx) mode. Even though an admin user is part of AG, these non-elevated processes **do not have authority** to access resources that are locked only to AG. 

Any misconfigured permissions would manifest as an attention seeking log entry. Ex. if a private key is not protected, you'll see the following:
```Powershell
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'ssh_host_dsa_key' are too open.
```

## Server side resources
### Host private key files
Host keys represent host's identity. To prevent unauthorized access to these files, host keys need to be owned by SY or AG. No other user should have access to host key files. Following is a misconfigured host private key because 'otheruser' owns it and has access to the key. 
```Powershell
PS C:\>(get-acl .\ssh_host_dsa_key).owner
otheruser
PS C:\>icacls .\ssh_host_dsa_key
ssh_host_dsa_key   NT AUTHORITY\SYSTEM:(F)
                   BUILTIN\Administrators:(F)
                   otheruser:(R) 
```
Steps to fix these permissions
```Powershell
PS C:\>icacls .\ssh_host_dsa_key /setowner system
PS C:\>icacls .\ssh_host_dsa_key /remove otheruser
```
At this point, you could do the following to replicate these permissions onto other host keys
```Powershell
PS C:\>get-acl .\ssh_host_dsa_key | Set-Acl ssh_host*key
```
### authorized_keys
authorized_keys is an user associated file that represents a list of authorized public keys that could be used for (key-based) user authentication. Unauthorized access to this file compromises the associated user's account. This file should not be owned by, nor provide access to any other user. 
Following is a misconfigured authorized key because 
- 'otheruser1' has access to the file (through inheritance) 
- 'otheruser2' has access to this file (explicit permission). 
```Powershell
PS C:\>(get-acl .\users\thisuser\.ssh\authorized_keys).owner
thisuser
PS C:\>icacls .\users\thisuser\.ssh\authorized_keys
ssh_host_dsa_key   BUILTIN\Administrators:(F)
                   thisuser:(F) 
                   otheruser1:(IR)
                   otheruser2:(R)
```
Steps to fix these permissions - remove inheritance and inherited permissions
```Powershell
PS C:\>icacls .\users\thisuser\.ssh\authorized_keys /inheritance:r
PS C:\>icacls .\users\thisuser\.ssh\authorized_keys /remove otheruser2
```
### administrators_authorized_keys
Default location for authorized keys file for users in administrators group is 
`%programdata%\ssh\administrators_authorized_keys`
This file should only be accessible by SYSTEM and Administrators group.

Steps to fix permissions on this file:
```Powershell
PS C:\>icacls administrators_authorized_keys /inheritance:r
PS C:\>icacls administrators_authorized_keys /grant SYSTEM:`(F`)
PS C:\>icacls administrators_authorized_keys /grant BUILTIN\Administrators:`(F`)
```


## Client side resources
### User private key files
User's private keys are user's credentials. To prevent unauthorized access to these files, private keys need to be owned by the user and no other user should have access to user's key files.
### ssh_config
User level default ssh_config is located in user's profile (~/.ssh/config). This has similar restrictions as the user's private keys described above.  

