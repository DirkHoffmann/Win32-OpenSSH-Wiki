#### Download Latest Source
  - git clone https://github.com/PowerShell/openssh-portable
  - git checkout latestw_all

#### Building OpenSSH for Windows Using Visual Studio, 2015 or newer [*Recommended*]
  - Download and Install VS 2015, or newer, with Desktop Development with C++ - [latest install here](https://visualstudio.microsoft.com/downloads/)  
  - Install Windows SDK 10.0.17663.0 during Visual Studio install, or download from [here](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive/)
  - Install Microsoft Build Tools 2015 during Visual Studio install, or download from [here](https://www.microsoft.com/en-us/download/details.aspx?id=48159). Note, Build Tools 2015 are needed regardless of the Visual Studio version installed 
  - Open "contrib\win32\openssh\Win32-OpenSSH.sln" in Visual Studio, ensure platform toolset is set to "no upgrade" and Windows SDK is set to "10.0.17663.0"
  - If necessary, change the configuration and architecture from the middle toolbar
  - Build the Win32-OpenSSH binaries

#### Building OpenSSH for Windows Using Build Script
In Powershell:
  - cd repository-root
  - ipmo .\contrib\win32\openssh\OpenSSHBuildHelper.psm1 -Force
  - Start-OpenSSHBuild -Configuration <Release|Debug> -NativeHostArch <x64|x86>

#### Deploying OpenSSH for Windows
  - Start-OpenSSHPackage -Configuration <Release|Debug> -NativeHostArch <x64|x86>
  - Above generates Zipped binary and symbols payload. Follow further installation instructions [here](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH).

