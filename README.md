# Invoke-SMBLogin #
Validates username &amp; password combination(s) across a host or group of hosts using the SMB protocol.


## Using Invoke-SMBLogin with Powershell Empire ##

To use Invoke-SMBLogin from a Powershell Empire agent, have have to copy the Powershell script and the Empire module python script to the Empire folder:

- Invoke-SMBLogin.ps1 to **data/module_source/situational_awareness/network/**
- smblogin.py to **lib/modules/powershell/situational_awareness/network/**
