# apt

[TOC]

## setup proxy

sudo vi /etc/apt/apt.conf
```
Acquire::http::proxy "http://www-proxy.lmera.ericsson.se:8080";
Acquire::ftp::proxy "ftp://www-proxy.lmera.ericsson.se:8080";
Acquire::https::proxy "https://www-proxy.lmera.ericsson.se:8080";
```
需要重启虚拟机