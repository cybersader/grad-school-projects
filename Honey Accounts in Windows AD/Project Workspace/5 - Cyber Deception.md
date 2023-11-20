# Lab Overview
This lab will demonstrate the ease of creating detection for some common attacks using various deception techniques.  
**Please make the following considerations.**  
- This lab requires Active Directory modules for PowerShell  
- Should you choose to complete the installation of the remote server administration tools on the workstation, these labs will work from either server  
- **If you do not complete the RSAT install**, using PowerShell from the domain controller
## Objectives
- Installation of RSAT (Remote Server Administration Tools) for Windows 10 to accomplish this task.  
- Issues with RSAT:
	- Pre-requisite services are required as of January 25, 2022
	- #DO-TODO
## Methodology
- Install PS dependencies on Windows 10 system
- Then we Add new user Objects that we control
- We then deploy Deception
- Using Deception we create a decoy user and computer
- We then make the new accounts look interesting to an attacker
## Which Computer?
- Run on workstation, but use PowerShell in DC if that doesn't work
# Preparation: Add DS Tools (RSAT)
First, use PowerShell Components to add RSAT for Windows 10
```powershell
Add-WindowsCapability -Name Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0 -Online
```

- Results
	- ![](IMG-20231118203854173.png)
	- ![](IMG-20231118212605622.png)

# Create Controlled Objects
```powershell
New-ADUser -UserPrincipalName Luis.Graves@doazlab.com -Path "OU=DomainUsers,dc=doazlab,DC=com" -GivenName "Luis" -Surname "Graves" -Enabled 1 -Name "Luis.Graves" -desc "Accounting Controller" -office "Accounting" -title "Controller" -company "DevLabs" -AccountPassword (ConvertTo-SecureString "Password1!" -AsPlainText -Force) -Credential $Cred
```