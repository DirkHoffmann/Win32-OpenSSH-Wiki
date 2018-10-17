## You need to download and install:
* [Win32_OpenSSH](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)
* [Git for Windows](https://git-scm.com/download/win), selecting the "Run Git and included Unix tools from the Windows Command Prompt" when prompted. This option will install a bin folder in Program Files\git that will be placed into your path thus taking possibly taking precedence over other tools.
## On Server
1. Set system environment variable for sshd to pick up the git commands
     ```powershell
     $gitPath = Join-Path -Path $env:ProgramFiles -ChildPath "git\mingw64\bin"
     $machinePath = [Environment]::GetEnvironmentVariable('Path', 'MACHINE')
     [Environment]::SetEnvironmentVariable('Path', "$gitPath;$machinePath", 'Machine')
     ```
1. Restart sshd so the changes to the `Path` environment variable can take effect.
1. Create Windows users for all Git users.
1. Create a central Git repository. Go to where you want to create a central repo, `git clone --bare <source dir>`. A directory with name `<source dir>.git` will be created. In it will be the .git contents of your source dir repo. for example:

     `git clone --bare c:\git\newrepo.git`
1. If you already have user private and public keys, copy the user public key to `C:\Users\{user}\.ssh\` and rename it to authorized_keys
## On Client
1. Set environment variable for git to use Win32_OpenSSH

     `$env:GIT_SSH_COMMAND = '"C:\Program Files\OpenSSH\ssh.exe" -T'`
1. (Optional) For key based authentication to work, generate user private and public key. The generated public key need to copy to C:\Users\{user}\.ssh\authorized_keys as indicated in step 5 on Server

     `ssh-keygen.exe -t ed25519 -f c:\test\myprivatekey`
1. (Optional) Register the user private key for single sign on

     `ssh-add.exe c:\test\myprivatekey`
1. To check out a repository, go to where you want to put your local repo,

**Note that `git clone user@domain@servermachine:C:/test/myrepo.git` does not work due to [known issue](https://github.com/PowerShell/Win32-OpenSSH/issues/895). Work around it to set powershell as defaultShell in registry.
Or
by following steps when cmd is default shell:

     cd c:\mygitrepros
     # initialize a local repo folder
     git init mylocalrepo
     cd mylocalrepo
     # add the remote repro
     git remote add origin user@domain@servermachine:C:/test/myrepo.git
     # work around the known issue by launching powershell to run the git commands
     git config --local remote.origin.uploadpack "powershell git-upload-pack"
     git config --local remote.origin.receivepack "powershell git-receive-pack"
     git fetch origin

