To migrate sshd configuration from older versions (0.0.X.X):

- To use existing customized sshd_config, you need to copy it from binary location to %programdata%\ssh\sshd_config (Note that %programdata% is a hidden directory).
- To use existing host keys, you need to copy them from binary location to %programdata%\ssh\
- Prior versions required SSHD resources (sshd_config, host keys and authorized_keys) to have READ access to "NT Service\SSHD". This is no longer a requirement and the corresponding ACL entry should be removed. You may run `Powershell.exe -ExecutionPolicy Bypass -Command '. .\FixHostFilePermissions.ps1 -Confirm:$false'` (Note the first "." is a call operator.) to fix up these permissions.
