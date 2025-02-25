# Huawei Switch Command Documentation

---

## **Reset Switch**

To reset the switch and erase the saved configuration:

```shell
<HUAWEI> reset saved-configuration
Warning: The action will delete the saved configuration on the device.
The configuration will be erased to reconfigure. Continue? [Y/N]: y
```

---

## **Show IP Brief**

To display the summary of all the switch's IP interfaces:

```shell
display ip interface brief
```

---

## **Assign IP on Default VLAN**

To assign an IP address to the default VLAN (Vlanif1):

```shell
interface Vlanif1
ip address 192.168.12.31 255.255.255.0
```

Assign IP from DHCP:

```shell
interface Vlanif1
ip address dhcp-alloc
```

---

## **Up/No Shutdown VLAN**

To configure an interface to access mode, assign it to VLAN 1, and bring the port up:

```shell
[Huawei-SL3] interface ge 1/0/1
[Huawei-SL3-GE1/0/1] port link-type access
[Huawei-SL3-GE1/0/1] port default vlan 1
[Huawei-SL3-GE1/0/1] undo shutdown
[Huawei-SL3-GE1/0/1] quit
```

---

## **Create Local User**

To create a local user with a password and assign privilege level 3 (Admin privileges):

```shell
[Huawei-SL3] aaa
[Huawei-SL3-aaa] local-user iamreadoy password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user iamreadoy privilege level 3
[Huawei-SL3-aaa] local-user iamreadoy service-type ?
```

---

## **Show All User**

```shell
[Huawei-SL3-aaa] display local-user
```

---

## **Delete a User**

```shell
[Huawei-SL3-aaa] undo local-user iamreadoy
```

---

## **Specify Service for Local User**

SSH-enabled user account:

```shell
[Huawei-SL3-aaa] local-user adminssh password irreversible-cipher Admin@24
[Huawei-SL3-aaa] local-user adminssh privilege level 3
Warning: This operation may affect online users and will change the user privilege level, Continue? [Y/N]: y
[Huawei-SL3-aaa] local-user adminssh service-type ssh
```

Specify multiple services for user:

```shell
[Huawei-SL3-aaa] local-user adminssh service-type ssh http telnet ftp
```

---

## **Show User and Service**

```shell
[Huawei-SL3-aaa] display local-user username adminssh
```

---

## **Enable/Disable POE (Power over Ethernet)**

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

## **Add Description to a Switch Port**

```shell
[Huawei-SL3]interface range GE 1/0/1 to GE 1/0/8
[Huawei-SL3-port-group]description Poe Turned On
```

## **Show Description:**

```shell
[Huawei-SL3-port-group]display interface description
```

---

## **Display Log**

```shell
<HUAWEI>terminal monitor
<HUAWEI>display logbuffer
```

---

## **Filter Log**

```shell
<HUAWEI>display logbuffer module debug
```

---

## **SnmpWalk**

### Enable SNMP:
```shell
[HUAWEI]snmp-agent
```

### Enable SNMP v2c:
```shell
[HUAWEI]snmp-agent sys-info version v2c
```

### Create Community String:
```shell
[HUAWEI]snmp-agent community read public
```

### Allow Interface for SNMP:
```shell
[HUAWEI]snmp-agent protocol source-interface Vlanif 1
```

---

## **Backup Configuration**

```shell
<Huawei-SL3>save backup.cfg
```

---

## **Enable FTP Server and Login from Windows**

```shell
ftp> get flash:/config.cfg backup.cfg
```

---

## **Restore Configuration**

```shell
<HUAWEI>startup saved-configuration config.cfg
```

---

## **Restart the Device**

```shell
<HUAWEI>reboot
```

---

*This concludes the key commands for managing Huawei switches.*

