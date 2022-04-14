
## Login With Password

1. Workgroup users
     * `ssh user@host`
2. Domain users: Prior to v7.7.0.0, domain needs to be explicitly specified. Any of the following formats work
     * `ssh -l user@domain host`
     * `ssh domain\user@host`
     * `ssh user@domain@host`
     * `ssh user@host` (works from v7.7.0.0 onwards provided `user` has no conflicts otherwise - ex. `user` exists both on local account data base and on domain)


## Login With SSH Keys

### Usage from client-side (`ssh`)

1. Generate a key pair on the client (preferably with a passphrase):
     * `ssh-keygen -t rsa -f id_rsa`
2. Register private key with ssh-agent (optional, for single sign-on experience)
     * `net start ssh-agent`
     * `ssh-add id_rsa` 
3. Login using private key
     * `ssh -i .\id_rsa user@host` (workgroup user)
     * `ssh -i .\id_rsa -l user@domain host` (domain user)

### Setup server-side (`sshd`)

1. Append contents of `id_rsa.pub` (client's public key) to the following file in corresponding user's directory `%systemdrive%\Users\<user>\.ssh\authorized_keys` (create one if needed). 
2. Double check access permissions on authorized_keys (only System, Administrators and owner can have access).
`icacls %systemdrive%\Users\<user>\.ssh\authorized_keys`

## Login using Kerberos Authentication
### Setup server-side
1. On a domain joined server, set GSSAPIAuthentication to `yes` in sshd_config
2. If you modify the sshd_config then restart the sshd service
     * `net stop sshd`
     * `net start sshd`


### Usage on a domain joined Windows client logged in as domain user

* `ssh -K host`

**Please note you have to use the hostname instead of the username.**

### For Unix and Linux users

The [Modern Unix Rosetta Stone](https://certsimple.com/rosetta-stone) includes PowerShell examples of common Unix and Linux commands. 

[Secure file]: https://github.com/PowerShell/Win32-OpenSSH/wiki/Security-protection-of-various-files-in-win32-openssh
