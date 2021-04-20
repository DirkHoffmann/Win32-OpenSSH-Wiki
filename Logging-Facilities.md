### Logging facilities
Prior to v7.6.1.0, server side components supported only 1 logging facility (file based at logs\sshd.log). 
In v7.6.1.0 and later, ETW logging is added and is the default. You can view these logs under event viewer as follows:


![image](https://user-images.githubusercontent.com/14185020/37054957-4c6b2d4e-2135-11e8-90e3-3eba472ffc46.png)

The admin channel is for CRITICAL and ERROR events, operational is for INFO and debug is for DEBUG* variants.
The payload would mimic what users would otherwise see in a typical syslog entry. 

To see Debug logs in EventViewer, do the following:
- Ensure sshd_config has logging level at DEBUG or above
- In Eventviewer, select option to show "Analytic and Debug Logs" (under top menu, View)
- Enable Debug logging (select Debug channel, click "Enable log" on right menu) 

#### File based logging 
File based logging option (useful for quickly collecting debug traces) can be turned on by setting the following in sshd_config

 `SyslogFacility LOCAL0 `

 `LogLevel Debug3 `

Restart the sshd service after making changes to sshd_config.

 `net stop sshd`

 `net start sshd`

With this option, the logs would be collected at %programdata%\ssh\logs.


sftp-server would follow similar semantics for logging (by default to ETW) and to files using the following as subsystem path in sshd_config:

`sftp-server -f LOCAL0 -l DEBUG3`

Restart the sshd service after making changes to sshd_config. sftp-server logs will be written to %programdata%\ssh\logs\sftp-server.log