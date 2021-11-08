# RSAT Tools Install Failed

Due to Windows Update settings by default download and install the tools from WSUS, you will face the installation failed. First of all, you required to disable the WSUS and allow Windows to download the tools directly from Microsoft online server.
```
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "UseWUServer" -Value 0
```
Then you need to restart the <i>wuauserv</i> services.
```
Restart-Service wuauserv
```
Start to install the RSAT tools with following command.
```
Add-WindowsCapability -Online -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0
```
Now enable back WSUS.
```
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU" -Name "UseWUServer" -Value 1
```
Finally you need to restart the <i>wuauserv</i> services.
```
Restart-Service wuauserv
```
