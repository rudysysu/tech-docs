# Network

vmware的NAT网络不但可以访问Internet，还可以被主机访问。

## 配置模板（来自k8s课程的例子）
```bash
TYPE=Ethernet
BOOTPROTO=static
IPADDR="{{ ansible_default_ipv4.address }}"
NETMASK="{{ ansible_default_ipv4.netmask }}"
GATEWAY="{{ ansible_default_ipv4.gateway }}"
DEFROUTE=yes
PEERDNS=yes
PEERROUTES=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
NAME=eth0
DEVICE=eth0
ONBOOT=yes
```

## DNS
```
DNS1=192.168.37.2
```

## Commands
```
ip a
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```
