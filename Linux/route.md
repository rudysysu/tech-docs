---
layout: docs
title: Route
permalink: /linux/route/
---

* toc
{: toc }

# add/del route

* route add -net 192.168.1.0/24 dev eth0
* route add -net 192.168.2.0/24 dev eth1
* route del -net 192.168.1.0/24 dev eth0
* route del -net 192.168.2.0/24 dev eth1

# add/del default route

* route add default gw 192.168.1.1
* route del default
