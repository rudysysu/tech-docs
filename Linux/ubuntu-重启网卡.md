先查看系统服务，VMWare的DHCP服务可能被关掉了，要启动下。

$ sudo ip link set enp0s3 down
$ sudo ip link set enp0s3 up