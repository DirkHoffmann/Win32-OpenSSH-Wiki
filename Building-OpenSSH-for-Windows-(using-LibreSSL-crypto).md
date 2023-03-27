#### Download Latest Source
  - git clone https://github.com/PowerShell/openssh-portable
  - git checkout latestw_all

#### Building OpenSSH for Windows Using Visual Studio, 2015 or newer [*Recommended*]
  - Download and Install VS 2015, or newer, with Desktop Development with C++ - [latest install here](https://visualstudio.microsoft.com/downloads/) 
     - Confirm the Desktop Development with C++ Kit was installed properly by checking `${env:ProgramFiles(x86)}\Microsoft Visual Studio\*\*\VC\Auxiliary\Build` for a `vcvarsall.bat` file, as shown in the image below: 
![C++ Development Kit Folder Location](https://user-images.githubusercontent.com/14894321/155555676-53815d5e-5fb0-48ed-b71d-d0a679cb276b.png)
- Install Windows SDK 10.0.17763.0 during Visual Studio install, or download from [here](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive/)
     - Confirm the SDK was installed properly by checking `${env:ProgramFiles(x86)}\Windows Kits\10\Bin` for a `10.0.17763.0` folder, as shown in the image below: 
![Windows 10 SDK Folder Location](https://user-images.githubusercontent.com/14894321/155553357-8961ac07-9671-4916-8ae2-8123ab2b892e.png)
- Install Microsoft Build Tools 2015 during Visual Studio install, or download from [here](https://www.microsoft.com/en-us/download/details.aspx?id=48159). Note, Build Tools 2015 are needed regardless of the Visual Studio version installed 
     - Confirm the Build Tools were installed properly by checking `${env:ProgramFiles(x86)}\MSBuild\Microsoft.Cpp\v4.0\140` for a `Microsoft.Cpp.Default.Props` file, as shown in the image below: 
![Microsoft Build Tools 2015 Folder Location](https://user-images.githubusercontent.com/14894321/155554939-43ffc96f-185e-427c-82de-16a3a60ce32a.png)
- Open "contrib\win32\openssh\Win32-OpenSSH.sln" in Visual Studio, ensure platform toolset is set to "no upgrade" and Windows SDK is set to "10.0.17763.0" as shown in the image below: \
![Visual Studio Initial Solution Settings](https://user-images.githubusercontent.com/14894321/155555889-9a2e617c-5f64-4178-b40d-e5231f42f302.png)
- If necessary, change the configuration and architecture from the middle toolbar
- Build the Win32-OpenSSH binaries
     - Binaries will be in a `.\bin\{Architecture}\{Configuration}` folder, as shown in the image below for an x64, Debug build:
![OpenSSH Binaries Folder Location](https://user-images.githubusercontent.com/14894321/155556691-3573b5df-8295-4815-9543-a8e38e78b5fa.png)

#### Building OpenSSH for Windows Using Build Script
In Powershell:
  - cd repository-root
  - ipmo .\contrib\win32\openssh\OpenSSHBuildHelper.psm1 -Force
  - Start-OpenSSHBuild -Configuration <Release|Debug> -NativeHostArch <x64|x86>

#### Deploying OpenSSH for Windows
  - Start-OpenSSHPackage -Configuration <Release|Debug> -NativeHostArch <x64|x86>
  - Above generates Zipped binary and symbols payload. Follow further installation instructions [here](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH).



