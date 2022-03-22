FIDO/U2F is supported in win32-openssh V8.9.0.0+.

* Make sure SYSTEM PATH environment variable has the Win32-OpenSSH V8.9.0.0+ folder path.

* Please note, **V8.9.0.0 MSI installation** has a bug related to FIDO. Refer to https://github.com/PowerShell/Win32-OpenSSH/issues/1914.

* Resident keys (SSH keys are stored on the hardware device). 
    * cd <openssh_bin_folder_path>
    * Create the resident keys

       `ssh-keygen.exe -t ecdsa-sk -f .\id-ecdsa-sk -O "resident"`

    * If you want to download the resident keys from the hardware device. Run in an **elevated administrator** terminal.

       `ssh-keygen.exe -K`

    * copy the public key (`.\id_ecdsa-sk[<GUID>].pub`) to authorized_keys file.

    * SSH connection must be successful

       `ssh.exe user@ip -i .\id_ecdsa-sk[<GUID>]`

    * register with ssh-agent

       `ssh-add.exe .\id_ecdsa-sk[<GUID>]
       ssh-add.exe -L`

    * SSH connection must be successful

       `ssh.exe user@ip`

* Non-resident keys (keys not stored on the hardware device)
    * cd <openssh_bin_folder_path>
    * Create the non-resident keys

       `ssh-keygen.exe -t ecdsa-sk -f .\id-ecdsa-sk`

    * copy the public key (`.\id_ecdsa-sk.pub`) to authorized_keys file.

    * SSH connection must be successful

       `ssh.exe user@ip -i .\id_ecdsa-sk`

    * register with ssh-agent

       `ssh-add.exe .\id_ecdsa-sk
       ssh-add.exe -l`

    * SSH connection must be successful

       `ssh.exe user@ip`