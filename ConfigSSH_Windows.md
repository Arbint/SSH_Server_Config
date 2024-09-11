# Configuration

On Windows, open powershell as Admin
and type in:
```
Add-WindowsCapability -Online -Name OpenSSH.Server
```
check installation
```
Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'
```

Make it Starts Automatically
```
Set-Service -Name sshd -StartupType 'Automatic'
```

And Finally Starts it:
```
Start-Service sshd
```

Verify the Service is running:
```
Get-Service -Name sshd
```
