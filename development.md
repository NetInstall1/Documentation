# Development Moves

## 1. Creating a Test Network

### Platform Selection
Choose a suitable platform for creating a test network. Options include:
- Virtual Machines using VMware/Oracle
- Windows Docker Images
- GCP/AWS/Azure Virtual Machines

### GCP Setup
Opting for GCP (Google Cloud Platform):
- Create 2-3 Windows instances on GCP.
- Install ZeroTier-cli on each instance.
- Create a ZeroTier Network and have all instances join this network.
- Join your local machine to the ZeroTier Network.
- Designate your local machine as the agent and GCP instances as guests.

## 2. Psexec Configuration

### Psexec Installation
Ensure that Psexec is installed on your local machine.

### Addressing "Access Denied" Error
To overcome the 'psexec: "Access denied"' error, execute the following commands in administrator mode:
```bash
reg add HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\system /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1 /f
```

```bash
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" /v AutoShareServer /t REG_DWORD /d 1 /f
```

```bash
netsh advfirewall firewall set rule name="File and Printer Sharing (SMB-In)" new enable=Yes profile=private,domain,public
```
## 3. Agent Configuration

## 4. User Creation
Create a common admin user in the network such that the agent can access the guests
```bash
#create user
net user username pass /add

#add the use to admin group
net localgroup Administrators /add username

#check whether the user is added to group
net localgroup Administrators
```


