# Ubuntu Install

## Network

### NAT + Host-only Adapter.

Type              |Access Internet |Access Other VM  | Access By Host
------------------|----------------|-----------------|----------------
NAT               |Y               |N                |By port forword
Host-only Adapter |N               |Y                |By direct access

### ifconfig -a
```bash
enp0s3    Link encap:Ethernet  HWaddr 08:00:27:89:59:ff  
          inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe89:59ff/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:17 errors:0 dropped:0 overruns:0 frame:0
          TX packets:36 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:2080 (2.0 KB)  TX bytes:2977 (2.9 KB)

enp0s8    Link encap:Ethernet  HWaddr 08:00:27:46:d7:df  
          inet addr:192.168.56.102  Bcast:192.168.56.255  Mask:255.255.255.0
          inet6 addr: fe80::a00:27ff:fe46:d7df/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:687 errors:0 dropped:0 overruns:0 frame:0
          TX packets:509 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:60176 (60.1 KB)  TX bytes:65006 (65.0 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:165 errors:0 dropped:0 overruns:0 frame:0
          TX packets:165 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1 
          RX bytes:12279 (12.2 KB)  TX bytes:12279 (12.2 KB)
```

### /etc/network/interfaces
```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp0s3
iface enp0s3 inet dhcp


auto enp0s8
iface enp0s8 inet static
address 192.168.56.102
netmask 255.255.255.0
gateway 192.168.56.1
```

### route
```bash
route del default gateway 192.168.56.1 dev enp0s8
route add default gateway 10.0.2.2 dev enp0s3

root@keycload-1:~# route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
0.0.0.0         10.0.2.2        0.0.0.0         UG    0      0        0 enp0s3
10.0.2.0        0.0.0.0         255.255.255.0   U     0      0        0 enp0s3
192.168.56.0    0.0.0.0         255.255.255.0   U     0      0        0 enp0s8
```

### /etc/hostname 
```bash
root@keycload-1:~# vim /etc/hostname 
keycload-2
```

### /etc/sudoers
```bash
# Allow members of group sudo to execute any command
#%sudo  ALL=(ALL:ALL) ALL
%sudo  ALL=(ALL:ALL) NOPASSWD:ALL
```