#### Download Latest Source
  - git clone https://github.com/PowerShell/openssh-portable
  - git checkout latestw_all

#### Building OpenSSH for Windows Using Visual Studio [*Recommended*]
  - Download and Install Visual Studio - [latest install here](https://visualstudio.microsoft.com/downloads/). 
    - If using the Visual Studio installer, select the following:
      - Desktop Development with C++ Workload
      - Windows 11 SDK 10.0.22621.0 Individual Component
      - MSVC 143 Build Tool(s) Individual Component(s) - up to 3 depending on which architecture(s) will be built: x86/x64, ARM, ARM64 
      - MSVC 143 Spectre-Mitigated Lib(s) Individual Component(s) - up to 3 depending on which architecture(s) will be built: x86/x64, ARM, ARM64

    - Confirm the selections look something like this: 
![Visual Studio Installer GUI](https://github.com/PowerShell/Win32-OpenSSH/assets/14894321/1966b3df-2c42-4eb6-a8b1-dad3bc84d095)

     - Confirm the Desktop Development with C++ Kit was installed properly by checking `${env:ProgramFiles}\Microsoft Visual Studio\*\*\VC\Auxiliary\Build` for a `vcvarsall.bat` file, as shown in the image below: 
![C++ Development Kit Folder Location](https://github.com/PowerShell/Win32-OpenSSH/assets/14894321/f27bf4cd-70fd-4c48-847c-41cf5cf4b0aa)

- Install Windows SDK 10.0.22621.0 during Visual Studio install, or download from [here](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive/)
     - Confirm the SDK was installed properly by checking `${env:ProgramFiles(x86)}\Windows Kits\10\Bin` for a `10.0.22621.0` folder, as shown in the image below: 
![Windows 10 SDK Folder Location](https://github.com/PowerShell/Win32-OpenSSH/assets/14894321/fbde27f5-3f2e-4ded-9733-61b1279f06ac)

- Confirm the Build Tools were installed properly by checking `${env:ProgramFiles}\Microsoft Visual Studio\2022\*\MSBuild\Microsoft\VC\v170` for a `Microsoft.Cpp.Default.Props` file, as shown in the image below: 
![Microsoft Build Tools 2022 Folder Location](https://github.com/PowerShell/Win32-OpenSSH/assets/14894321/4e8b0f24-2ef1-4d4a-8c60-b580d425fe89)
- Open `contrib\win32\openssh\Win32-OpenSSH.sln` in Visual Studio, if prompted ensure platform toolset is set to "no upgrade" and Windows SDK is set to "10.0.22621.0" 
- If necessary, change the configuration and architecture from the middle toolbar
- Build the Win32-OpenSSH binaries
- Note: after the first build of a configuration & architecture or if a new libcrypto version is being pulled in, the corresponding `libcrypto.dll` needs to be copied from `\contrib\win32\openssh\libressl\bin\desktop\{Architecture}\` to `.\bin\{Architecture}\{Configuration}`
     - Binaries will be in a `\bin\{Architecture}\{Configuration}` folder, as shown in the image below for an x64, Debug build:
![OpenSSH Binaries Folder Location](https://user-images.githubusercontent.com/14894321/155556691-3573b5df-8295-4815-9543-a8e38e78b5fa.png)


#### Building OpenSSH for Windows Using Build Script
In Powershell:
  - cd repository-root
  - ipmo .\contrib\win32\openssh\OpenSSHBuildHelper.psm1 -Force
  - Start-OpenSSHBuild -Configuration <Release|Debug> -NativeHostArch <x64|x86|ARM|ARM64>

#### Deploying OpenSSH for Windows
  - Start-OpenSSHPackage -Configuration <Release|Debug> -NativeHostArch <x64|x86|ARM|ARM64>
  - Above generates Zipped binary and symbols payload. Follow further installation instructions [here](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH).



