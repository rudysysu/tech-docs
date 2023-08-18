## ubuntu 20.04
```
rudy@u64:~$ cat /etc/netplan/00-installer-config.yaml 
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp0s5:
      dhcp4: false
      addresses: [10.211.55.101/24]
      gateway4: 10.211.55.1
      nameservers: 
        addresses: [114.114.114.114]
  version: 2


root@u64:~# netplan apply


root@u64:~# ifconfig
enp0s5: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.211.55.101  netmask 255.255.255.0  broadcast 10.211.55.255
        inet6 fe80::21c:42ff:feb9:27b5  prefixlen 64  scopeid 0x20<link>
        inet6 fdb2:2c26:f4e4:0:21c:42ff:feb9:27b5  prefixlen 64  scopeid 0x0<global>
        ether 00:1c:42:b9:27:b5  txqueuelen 1000  (Ethernet)
        RX packets 188200  bytes 265057323 (265.0 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 44182  bytes 2495250 (2.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
