## Configuration
```bash
[root@localhost ~]# cat /etc/sysconfig/network-scripts/ifcfg-ens33 
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static"
IPADDR="192.168.37.132"
NETMASK="255.255.255.0"
GATEWAY="192.168.37.2"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="5e353eb4-4c1a-49d6-bc86-14a1386d2268"
DEVICE="ens33"
ONBOOT="yes"

DNS1=192.168.37.2
```

## Restart
```bash
/etc/init.d/network restart
systemctl restart network
```
