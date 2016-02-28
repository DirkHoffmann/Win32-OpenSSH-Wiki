####Follow these Powershell steps to retrieve links to latest packages:

`$url = 'https://github.com/PowerShell/Win32-OpenSSH/releases/latest/'`  
`$request = [System.Net.WebRequest]::Create($url)`  
`$request.AllowAutoRedirect=$false`  
`$response=$request.GetResponse()`  
`$([String]$response.GetResponseHeader("Location")).Replace('tag','download') + '/OpenSSH-Win64.zip'`  
`$([String]$response.GetResponseHeader("Location")).Replace('tag','download') + '/OpenSSH-Win32.zip'`