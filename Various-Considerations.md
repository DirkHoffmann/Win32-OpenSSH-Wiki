Following issues/limitations need to be considered while evaluating Win32 OpenSSH
- Cygwin users - Win32 OpenSSH service name (sshd) conflict with Cygwin's version of OpenSSH daemon prior to version 8.0, 
You may host Cygwin's OpenSSH daemon along side Win32's version by registering the later with a different name (say win32sshd), by doing the following in elevated Powershell
```
sc.exe delete sshd
New-Service -Name win32sshd -BinaryPathName 'C:\Program Files\OpenSSH\sshd.exe' -StartupType Manual
```
- [Elevation of Privilege over loopback](https://github.com/PowerShell/Win32-OpenSSH/issues/680) on misconfigured machines.
- ssh-agent only supports '-l' '-L' 'd' and '-D' options. It ignores '-c' and '-t' options of ssh-add. It persistently and permanently stores the user's private key.
- Text resources (config and key files) need to be either ASCII or UTF-8 (UTF-16 variants are not supported)
- On Windows 10, if you've [enabled Developer Mode](https://docs.microsoft.com/en-us/windows/uwp/get-started/enable-your-device-for-development), you probably have another implementation of SSH installed on your machine.
To figure out if this is the case, look for TCP port bindings on port 22 and these services: “SSH Server Broker” and “SSH Server Proxy”
    * `netstat -anop TCP`
    * If you do see 22 occupied, [#610](https://github.com/PowerShell/Win32-OpenSSH/issues/610) has workarounds to deal with port conflict. 

- SFTP doesn't support chmod