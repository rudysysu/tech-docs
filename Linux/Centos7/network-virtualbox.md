# Network

## NAT: For access Internet
```bash
[root@localhost network-scripts]# pwd
/etc/sysconfig/network-scripts
[root@localhost network-scripts]# cat ifcfg-enp0s3
BOOTPROTO=dhcp
DEVICE=enp0s3
ONBOOT=yes
```

## Host-only Adapter: For accessed by Host
```bash
[root@localhost network-scripts]# pwd
/etc/sysconfig/network-scripts
[root@localhost network-scripts]# cat ifcfg-enp0s8
HWARRD="08:00:27:74:92:38"
TYPE=Ethernet
BOOTPROTO=static
IPADDR=192.168.56.151
NETMASK=255.255.255.0
NM_CONTROLLED=no
DEVICE=enp0s8
ONBOOT=yes
```

## Commands
```
ip addr
/etc/init.d/network restart
systemctl restart network.service
systemctl status network.service
```
