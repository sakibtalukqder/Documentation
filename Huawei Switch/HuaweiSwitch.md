# Huawei Switch Command Documentation

---

## Index

- [Huawei Switch Command Documentation](#huawei-switch-command-documentation)
  - [Index](#index)
  - [Reset Switch](#reset-switch)
  - [Show IP Brief](#show-ip-brief)
  - [Assign IP on Default VLAN](#assign-ip-on-default-vlan)
  - [Up/No Shutdown VLAN](#upno-shutdown-vlan)
  - [Create Local User](#create-local-user)
  - [Show All Users](#show-all-users)
  - [Delete a User](#delete-a-user)
  - [Specify Service for Local User](#specify-service-for-local-user)
  - [Show User and Service](#show-user-and-service)
  - [Enable/Disable POE (Power over Ethernet)](#enabledisable-poe-power-over-ethernet)
  - [Add Description to a Switch Port](#add-description-to-a-switch-port)
  - [Show Description](#show-description)
  - [Display Log](#display-log)
  - [Filter Log](#filter-log)
  - [Send Log to Remote Server](#send-log-to-remote-server)
  - [SNMP Walk](#snmp-walk)
  - [Backup Configuration](#backup-configuration)
  - [Enable FTP Server and Login from Windows](#enable-ftp-server-and-login-from-windows)
  - [Restore Configuration](#restore-configuration)
  - [Firmware Update](#firmware-update)
  - [Restart the Device](#restart-the-device)
  - [Chenge Console Password](#chenge-console-password)

---

## Reset Switch

To reset the switch and erase the saved configuration:

```shell
<HUAWEI> reset saved-configuration
Warning: The action will delete the saved configuration on the device.
The configuration will be erased to reconfigure. Continue? [Y/N]: y
```


---

## Show IP Brief

To display the summary of all the switch's IP interfaces:

```shell
display ip interface brief
```


---

## Assign IP on Default VLAN

To assign an IP address to the default VLAN (Vlanif1):

```shell
interface Vlanif1
ip address 192.168.12.31 255.255.255.0
```

To assign an IP from DHCP:

```shell
interface Vlanif1
ip address dhcp-alloc
```


---
---
---

## Up/No Shutdown VLAN

To configure an interface to access mode, assign it to VLAN 1, and bring the port up:

```shell
[Huawei-SL3] interface ge 1/0/1
[Huawei-SL3-GE1/0/1] port link-type access
[Huawei-SL3-GE1/0/1] port default vlan 1
[Huawei-SL3-GE1/0/1] undo shutdown
[Huawei-SL3-GE1/0/1] quit
```


---

## Create Local User

To create a local user with a password and assign privilege level 3 (Admin privileges):

```shell
[Huawei-SL3] aaa
[Huawei-SL3-aaa] local-user iamreadoy password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user iamreadoy privilege level 3
[Huawei-SL3-aaa] local-user iamreadoy service-type ?
```


---

## Show All Users

```shell
[Huawei-SL3-aaa] display local-user
```


---

## Delete a User

```shell
[Huawei-SL3-aaa] undo local-user iamreadoy
```


---

## Specify Service for Local User

SSH-enabled user account:

```shell
[Huawei-SL3-aaa] local-user adminssh password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user adminssh privilege level 3
[Huawei-SL3-aaa] local-user adminssh service-type ssh
```

Specify multiple services for a user:

```shell
[Huawei-SL3-aaa] local-user adminssh service-type ssh http telnet ftp  
```

Specify FTP Directory for an FTP user (if needed):

```shell
[Huawei-SL3-aaa] local-user ftpuser ftp-directory flash:/
```


---

## Show User and Service

```shell
[Huawei-SL3-aaa] display local-user username adminssh
```


---

## Enable/Disable POE (Power over Ethernet)

Enable POE:

```shell
[Huawei-SL3] interface ge1/0/3
[Huawei-SL3-GE1/0/3] poe enable
```

Disable POE:

```shell
[Huawei-SL3-GE1/0/3] undo poe enable
Warning: This operation will power off the PD connected to this port. Continue? [Y/N]: y
```


---

## Add Description to a Switch Port

```shell
[Huawei-SL3]interface range GE 1/0/1 to GE 1/0/8
[Huawei-SL3-port-group]description Poe Turned On
```


---

## Show Description

```shell
[Huawei-SL3-port-group]display interface description
```


---

## Display Log

```shell
<HUAWEI>terminal monitor
Info: Current terminal monitor is on.

<HUAWEI>display logbuffer
```


---

## Filter Log

```shell
<HUAWEI>display logbuffer module ?
```

---

## Send Log to Remote Server

```shell
info-center enable
info-center source default channel 2
info-center loghost 192.168.3.115
```

---

## SNMP Walk

Enable SNMP:

```shell
[HUAWEI]snmp-agent
```


---

## Backup Configuration

```shell
<Huawei-SL3>save backup.cfg
```


---

## Enable FTP Server and Login from Windows

```shell
[Huawei-SL3-aaa] local-user ftpuser ftp-directory flash:/
```


---

## Restore Configuration

```shell
<HUAWEI>startup saved-configuration config.cfg
```


---

## Firmware Update

```shell
<HUAWEI>startup system-software flash:/<filename.cc>
```


---

## Restart the Device

```shell
<HUAWEI>reboot
```

## Chenge Console Password

```shell
<HUAWEI>system-view
[HUAWEI]user-interface console 0
[HUAWEI-ui-console0]set authentication password cipher NetAdminOpl@2025
[HUAWEI-ui-console0]authentication-mode password
Warning: The "password" authentication mode is not secure, and it is strongly recommended to use "aaa" authentication mode.
[HUAWEI-ui-console0]quit
```