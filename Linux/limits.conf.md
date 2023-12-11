# limits.conf

[TOC]

## Part1
/etc/security/limits.conf.


set ulimit -n 65536 as root
or set nofile to 65536 in /etc/security/limits.conf.

*       soft    nofile  65536
*       hard    nofile  65536