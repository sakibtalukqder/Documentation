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
  - [Send Log to Remote Server](#send-log-to-remote-server)
  - [Filter Log](#filter-log)
  - [SNMP Walk](#snmp-walk)
  - [Backup Configuration](#backup-configuration)
  - [Enable FTP Server and Login from Windows](#enable-ftp-server-and-login-from-windows)
  - [Restore Configuration](#restore-configuration)
  - [Firmware Update](#firmware-update)
  - [Restart the Device](#restart-the-device)

---

## Reset Switch

To reset the switch and erase the saved configuration:

```shell
<HUAWEI> reset saved-configuration
Warning: The action will delete the saved configuration on the device.
The configuration will be erased to reconfigure. Continue? [Y/N]: y
```

[Back to Index](#index)

---

## Show IP Brief

To display the summary of all the switch's IP interfaces:

```shell
display ip interface brief
```

[Back to Index](#index)

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

[Back to Index](#index)

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

[Back to Index](#index)

---

## Create Local User

To create a local user with a password and assign privilege level 3 (Admin privileges):

```shell
[Huawei-SL3] aaa
[Huawei-SL3-aaa] local-user iamreadoy password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user iamreadoy privilege level 3
[Huawei-SL3-aaa] local-user iamreadoy service-type ?
```

[Back to Index](#index)

---

## Show All Users

```shell
[Huawei-SL3-aaa] display local-user
```

[Back to Index](#index)

---

## Delete a User

```shell
[Huawei-SL3-aaa] undo local-user iamreadoy
```

[Back to Index](#index)

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

[Back to Index](#index)

---

## Show User and Service

```shell
[Huawei-SL3-aaa] display local-user username adminssh
```

[Back to Index](#index)

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

[Back to Index](#index)

---

## Add Description to a Switch Port

```shell
[Huawei-SL3]interface range GE 1/0/1 to GE 1/0/8
[Huawei-SL3-port-group]description Poe Turned On
```

[Back to Index](#index)

---

## Show Description

```shell
[Huawei-SL3-port-group]display interface description
```

[Back to Index](#index)

---

## Display Log

```shell
<HUAWEI>terminal monitor
Info: Current terminal monitor is on.

<HUAWEI>display logbuffer
```

[Back to Index](#index)

---

## Send Log to Remote Server

```shell
info-center enable
info-center source default channel 2
info-center loghost 192.168.3.115
```

[Back to Index](#index)

---

## Filter Log

```shell
<HUAWEI>display logbuffer module ?
```

[Back to Index](#index)

---

## SNMP Walk

Enable SNMP:

```shell
[HUAWEI]snmp-agent
```

[Back to Index](#index)

---

## Backup Configuration

```shell
<Huawei-SL3>save backup.cfg
```

[Back to Index](#index)

---

## Enable FTP Server and Login from Windows

```shell
[Huawei-SL3-aaa] local-user ftpuser ftp-directory flash:/
```

[Back to Index](#index)

---

## Restore Configuration

```shell
<HUAWEI>startup saved-configuration config.cfg
```

[Back to Index](#index)

---

## Firmware Update

```shell
<HUAWEI>startup system-software flash:/<filename.cc>
```

[Back to Index](#index)

---

## Restart the Device

```shell
<HUAWEI>reboot
```

[Back to Index](#index)

