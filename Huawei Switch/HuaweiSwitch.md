
# Huawei Switch Command Documentation

---

### Reset Switch

To reset the switch and erase the saved configuration:

```shell
<HUAWEI> reset saved-configuration
Warning: The action will delete the saved configuration on the device.
The configuration will be erased to reconfigure. Continue? [Y/N]: y
```

---

### Show IP Brief

To display the summary of all the switch's IP interfaces:

```shell
display ip interface brief
```

---

### Assign IP on Default VLAN

To assign an IP address to the default VLAN (Vlanif1):

```shell
interface Vlanif1
ip address 192.168.12.31 255.255.255.0
```
assign ip form dhcp
```shell
interface Vlanif1
ip address dhcp-alloc 
```

---

### Up/No Shutdown VLAN

To configure an interface to access mode, assign it to VLAN 1, and bring the port up:

```shell
[Huawei-SL3] interface ge 1/0/1
[Huawei-SL3-GE1/0/1] port link-type access
[Huawei-SL3-GE1/0/1] port default vlan 1
[Huawei-SL3-GE1/0/1] undo shutdown
[Huawei-SL3-GE1/0/1] quit
```

---

### Create Local User

To create a local user with a password and assign privilege level 3 (Admin privileges):

```shell
[Huawei-SL3] aaa
[Huawei-SL3-aaa] local-user iamreadoy password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user iamreadoy privilege level 3
[Huawei-SL3-aaa] local-user iamreadoy service-type ?
```

### Show All User

```shell
[Huawei-SL3-aaa] display local-user
```


### Delete a User

```shell
[Huawei-SL3-aaa] undo local-user iamreadoy
```


---

### Specify service for local user

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

Specify Ftp Directory for ftp user (if needed)
```shell
[Huawei-SL3-aaa] local-user ftpuser ftp-directory flash:/
```

---

### Show User and Service

To display information about the user and the associated service type:

```shell
[Huawei-SL3-aaa] display local-user username adminssh
```

---

### Enable/Disable POE (Power over Ethernet)

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
### Display Log
```shell
<HUAWEI>terminal monitor
Info: Current terminal monitor is on.

<HUAWEI>display logbuffer
Logging buffer configuration and contents : enabled
Allowed max buffer size : 10240
Actual buffer size : 512
Channel number : 4 , Channel name : logbuffer
Dropped messages : 0
Overwritten messages : 0
Current messages : 65

```

---
### Filter Log
```shell
<HUAWEI>display logbuffer module ?
  aaa            Feature name of log
  am             Feature name of log
  arp            Feature name of log
  bfd            Feature name of log
  bgp            Feature name of log
  ......

<HUAWEI>display logbuffer module debug
Logging buffer configuration and contents : enabled

```
---

### SnmpWalk

 ##### Enable snmp
 ```shell
    [HUAWEI]snmp-agent
    Info: It will create the SNMP listening socket after the source interface or source address is configured.
 ```
 
 ##### Install WEAKEA if rerquired 
 ```shell
    <3rd-Floor-R01-S02>install feature-software WEAKEA
    Info: Checking, please wait for a moment...done.
    Info: Start to install the package WEAKEA.
    Info: Operating, please wait for a moment..This operation will install weak algorithm software, and weak algorithms will be allowed to be used.
    .........done.
    Info: Succeeded in installing the software.
 ```
 
 ##### Enable Snmp Version v2c
 ```shell
    [HUAWEI]snmp-agent sys-info version ?
      all  Enable the device to support SNMPv1, SNMPv2c and SNMPv3
      v1   Enable the device to support SNMPv1
      v2c  Enable the device to support SNMPv2c
      v3   Enable the device to support SNMPv3
 ```
 ```shell
    [HUAWEI]snmp-agent sys-info version v2c
    Warning: SNMPv1/SNMPv2c is not secure, and SNMPv3 in either authentication or privacy mode is recommended.
    [HUAWEI]display snmp-agent sys-info
 ```

 ##### Create a community string
 ```shell
    [HUAWEI]snmp-agent community complexity-check disable
    Warning: Does not recommend to disable complexity check. A simple community name may result in security threats.

    [HUAWEI]snmp-agent community read ?
      STRING<1-32>  String of community name
      cipher        Specify community name with encrypted text

    [HUAWEI]snmp-agent community read public
 ```

 ##### Allow Interface for Snmp
 ```shell
    [HUAWEI]snmp-agent protocol source-interface Vlanif 1
        ----- Or Use All Interface instade of single interface -----
    [HUAWEI]snmp-agent protocol source all-interface
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

Specify Ftp Directory for ftp user (if needed)
```shell
[Huawei-SL3-aaa] local-user ftpuser ftp-directory flash:/
[R02-S02-5th-Floor]ftp server source -i Vlanif 1
Warning: FTP server source configuration will take effect in the next login. Continue? [Y/N]:y
Info: Succeeded in setting the source ip address of the FTP server to the ip address of Vlanif1.

```

login to ftp

```shell
C:\Documents and Setting\Administrator> ftp <switch ip>
Connected to 10.110.24.254.
220 FTP service ready.
User (10.110.24.254:(none)): username
331 Password required for huawei.
Password:
230 User logged in.
```
Set local Directory
```shell
ftp> binary
200 Type set to I.
ftp> lcd c:\temp
Local directory now C:\temp.
```

Download a file form switch thrugh ftp
```shell
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

### Firmware Update

Upload the firmware (both .cc and .PAT file) to the switch directory first and then execute this command
```shell
<HUAWEI>startup system-software ?
<HUAWEI>startup system-software flash:/<filename.cc>
```
Varify Update
```shell
<HUAWEI>display startup
MainBoard:
  Configured startup system software:        flash:/S310_V600R023C10SPC600.cc
  Startup system software:                   flash:/S310_V600R023C10SPC600.cc
  Next startup system software:              flash:/S310_V600R023C10SPC600.cc
  Startup saved-configuration file:          flash:/save.zip
  Next startup saved-configuration file:     flash:/save.zip
  Startup paf file:                          default
  Next startup paf file:                     default
  Startup patch package:                     NULL
  Next startup patch package:                NULL
  Startup feature software:                  NULL
  Next startup feature software:             NULL
```

### Restart the Device
```shell
<HUAWEI>reboot
```

This concludes the key commands for managing Huawei switches.
