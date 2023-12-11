# su

[TOC]

## Command
```bash
sudo su - reactor
sudo -iu rudy "/usr/local/elasticsearch/bin/elasticsearch" -d
```

## Problem

su: cannot set user id: Resource temporarily unavailable

```bash
vi /etc/security/limits.d/90-nproc.conf
	NOW
		*          soft    nproc     1024
		root       soft    nproc     unlimited
	TOBE
		*          soft    nproc     1024
		root       soft    nproc     unlimited
		reactor       soft    nproc     10240
```
