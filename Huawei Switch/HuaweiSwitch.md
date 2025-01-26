
# Huawei Switch Command Documentation

---

### 1. Reset Switch

To reset the switch and erase the saved configuration:

```shell
<HUAWEI> reset saved-configuration
Warning: The action will delete the saved configuration on the device.
The configuration will be erased to reconfigure. Continue? [Y/N]: y
```

---

### 2. Show IP Brief

To display the summary of all the switch's IP interfaces:

```shell
display ip interface brief
```

---

### 3. Assign IP on Default VLAN

To assign an IP address to the default VLAN (Vlanif1):

```shell
interface Vlanif1
ip address 192.168.12.31 255.255.255.0
```
assign ip form dhcp
```shell
interface Vlanif1
ip address 192.168.12.31 255.255.255.0
```

---

### 4. Up/No Shutdown VLAN

To configure an interface to access mode, assign it to VLAN 1, and bring the port up:

```shell
[Huawei-SL3] interface ge 1/0/1
[Huawei-SL3-GE1/0/1] port link-type access
[Huawei-SL3-GE1/0/1] port default vlan 1
[Huawei-SL3-GE1/0/1] undo shutdown
[Huawei-SL3-GE1/0/1] quit
```

---

### 5. Create Local User

To create a local user with a password and assign privilege level 3 (Admin privileges):

```shell
[Huawei-SL3] aaa
[Huawei-SL3-aaa] local-user iamreadoy password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user iamreadoy privilege level 3
[Huawei-SL3-aaa] local-user iamreadoy service-type ?
```

---

### 6. Specify service for local user

SSH-enabled user account:

```shell
[Huawei-SL3-aaa] local-user adminssh password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user adminssh privilege level 3
Warning: This operation may affect online users and will change the user privilege level, Continue? [Y/N]: y
[Huawei-SL3-aaa] local-user adminssh service-type ssh
Info: After changing the rights (including the password, access type, FTP directory, and HTTP directory) 
[Huawei-SL3-aaa]
```

Specify multiple service for user

```shell
[Huawei-SL3-aaa] local-user adminssh service-type  service-type ssh http telnet ftp  
Info: After changing the rights (including the password, access type, FTP directory, and HTTP directory) 
[Huawei-SL3-aaa]
```

---

### 7. Show User and Service

To display information about the user and the associated service type:

```shell
[Huawei-SL3-aaa] display local-user username adminssh
```

---

### 8. Enable/Disable POE (Power over Ethernet)

To enable or disable POE on a specific interface (e.g., GE1/0/3):

### Enable POE:
```shell
[Huawei-SL3] interface ge1/0/3
[Huawei-SL3-GE1/0/3] poe enable
```

### Disable POE:
```shell
[Huawei-SL3-GE1/0/3] undo poe enable
Warning: This operation will power off the PD connected to this port. Continue? [Y/N]: y
```

---
### Add Description to a switch port:
```shell
[Huawei-SL3]interface range GE 1/0/1 to GE 1/0/8
[Huawei-SL3-port-group]description Poe Turned On
```
---
### show Description:
```shell
[Huawei-SL3-port-group]display interface description
PHY: Physical
*down: administratively down
^down: standby
(l): loopback
(s): spoofing
(b): BFD down
(e): ETHOAM down
(d): Dampening Suppressed
(p): port alarm down
(dl): DLDP down
(c): CFM down
(ms): MACsec down
(ed): error down
Interface                     PHY     Protocol Description
GE1/0/1                       down    down     Poe Turned On
GE1/0/2                       down    down     Poe Turned On
GE1/0/3                       down    down     Poe Turned On
GE1/0/4                       down    down     Poe Turned On
GE1/0/5                       down    down     Poe Turned On
GE1/0/6                       down    down     Poe Turned On
GE1/0/7                       down    down     Poe Turned On
GE1/0/8                       down    down     Poe Turned On
GE1/0/9                       down    down
GE1/0/10                      down    down
GE1/0/11                      down    down
GE1/0/12                      down    down
GE1/0/13                      down    down
GE1/0/14                      down    down
GE1/0/15                      down    down
GE1/0/16                      down    down
GE1/0/17                      down    down
GE1/0/18                      down    down
GE1/0/19                      down    down
GE1/0/20                      down    down
GE1/0/21                      down    down
GE1/0/22                      down    down
GE1/0/23                      down    down
GE1/0/24                      up      up
GE1/0/25                      down    down
GE1/0/26                      down    down
GE1/0/27                      down    down
GE1/0/28                      down    down
NULL0                         up      up(s)
Vlanif1                       up      up
[Huawei-SL3-port-group]
```
---
### Backup Configuration
```shell
<Huawei-SL3>save backup.cfg
Warning: Are you sure to save the configuration to flash:/backup.cfg? [Y/N]:y
Warning: flash:/backup.cfg exists, overwrite? [Y/N]:y
Now saving the current configuration to the slot 1
Info: Save the configuration successfully.
```

### Enable FTP Server and Login from Windows
```shell
C:\Documents and Setting\Administrator> ftp 10.110.24.254
Connected to 10.110.24.254.
220 FTP service ready.
User (10.110.24.254:(none)): huawei
331 Password required for huawei.
Password:
230 User logged in.

ftp> binary
200 Type set to I.
ftp> lcd c:\temp
Local directory now C:\temp.

ftp> get flash:/config.cfg backup.cfg
```

### Restore Configuration
```shell
<HUAWEI>startup saved-configuration config.cfg
<HUAWEI>display startup
MainBoard:
  Configured startup system software:        cfcard:/device_software.cc
  Startup system software:                   cfcard:/device_software.cc
  Next startup system software:              cfcard:/device_software.cc
  Startup saved-configuration file:          cfcard:/config_old.cfg   //Current configuration file name.
  Next startup saved-configuration file:     cfcard:/config.cfg       //Name of the configuration file for the next startup.
  Startup paf file:                          default
  Next startup paf file:                     default
  Startup license file:                      default
  Next startup license file:                 default
  Startup patch package:                     NULL
  Next startup patch package:                NULL
```

### Restart the Device
```shell
<HUAWEI>reboot  //Restart the device.
```

This concludes the key commands for managing Huawei switches.
