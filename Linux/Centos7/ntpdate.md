# ntpdate
- ntp: this is the classic package, already existing in RHEL 6, RHEL 5, etc.
- chrony: this is a new solution better suited for portable PC or servers with network connection problems (time synchronization is quicker). chrony is the default package in RHEL 7.

## Server

### ntp
- install

```
yum install ntp
```

- config ntp.conf

````
vi /etc/ntp.conf

restrict 192.168.56.0 mask 255.255.255.0 nomodify notrap

server 0.asia.pool.ntp.org iburst
server 1.asia.pool.ntp.org iburst
server 2.asia.pool.ntp.org iburst
server 3.asia.pool.ntp.org iburst
```

- start service

```
systemctl enable/disable ntpd
systemctl start ntpd
ntpq -np
```

### chrony

- install

```
yum install chrony
```

- config chrony.conf

```
vi /etc/chrony.conf

server 0.rhel.pool.ntp.org iburst
server 1.rhel.pool.ntp.org iburst
server 2.rhel.pool.ntp.org iburst
server 3.rhel.pool.ntp.org iburst
```

- start service

```
systemctl enable/disable chronyd
systemctl start chronyd
chronyc sourcestats -v
chronyc sources -v
```

## Client

- install

```
yum install ntpdate
```

- start service

```
ntp -d asia.pool.ntp.org
ntp -u asia.pool.ntp.org
```

## example
- [chrony.conf](ntpdate/(design_lab)chrony.conf "design_lab")
- [ntp.conf](ntpdate/(design_lab)ntp.conf "design_lab")

## References
- https://www.tecmint.com/install-ntp-server-in-centos/
- http://www.pool.ntp.org/zone/asia