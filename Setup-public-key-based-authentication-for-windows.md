**Please note key based authentication is not supported for AAD users. Refer to https://github.com/PowerShell/Win32-OpenSSH/issues/1787.**

##  On the client machine, create the public/private key pair.
1) cd to <openssh_binary_folder>

2) Create the key pair.

      `ssh-keygen.exe -t rsa -f $env:USERPROFILE\.ssh\id_rsa`

      _Enter the passphrase (or) hit enter to skip the passphrase._


## On the server machine, execute the below commands.

1) Open the PowerShell window. **Admin users require elevated PowerShell window**.

2) Manually copy the public key to the server machine.

3) If you are an admin user and using default sshd_config then 

     i. Copy the public key

      `cp <public_key_absolute_path> "$env:programdata\ssh\administrators_authorized_keys"`
      
      _Please note administrators_authorized_keys is the file name without any extension._

     ii. set the right ACLs using one of the host private key file.
 
     `get-acl "$env:programdata\ssh\ssh_host_rsa_key" | set-acl "$env:programdata\ssh\administrators_authorized_keys"`


4) For non-admin users,

     copy the public key to authorized_keys file (without any extension).

       cp <public_key_absolute_path> $env:USERPROFILE\.ssh\authorized_keys
      _If you don't have .ssh folder under $env:USERPROFILE folder then manually create it_

## From the client machine, try the key-based authentication

    ssh user@domain@ip -i <private_key_absolute_path> (Domain users)
    ssh user@ip -i <private_key_absolute_path> (local users)

_Please note, if you have private_key in "$env:USERPROFILE\\.ssh" directory then you don't need to pass the private_key_absolute_path_

**_If you are using your own keys (instead of generating new ssh keys) then please make sure the file encoding is set to UTF-8**

