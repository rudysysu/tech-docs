---
layout: docs
title: SshTunnel
permalink: /linux/ssh-tunnel/
---

* toc
{: toc }

# Command

ssh -i XL_Key.pem -p 22 -N -f -C -g -L 11883:192.168.2.75:1883 cloud-user@192.168.2.75

* -i XL_Key.pem // 私钥
* -p 22  // 端口
* -N  // Do not execute a shell or command. 
* -f  // Fork into background after authentication. 
* -C  // Enable compression. 
* -g  // Allow remote hosts to connect to forwarded ports. 
* -L 11883:192.168.2.75:1883 // port:host:hostport 

# Example

~~~
device: ssh -i XL_Key.pem -p 22 -N -f -C -g -L 11883:192.168.2.75:1883 cloud-user@192.168.2.75
app:    ssh -i XL_Key.pem -p 22 -N -f -C -g -L 11884:192.168.2.75:1884 cloud-user@192.168.2.75
trip:   ssh -i XL_Key.pem -p 22 -N -f -C -g -L 48081:192.168.4.43:8081 centos@192.168.4.43
~~~

# mosquitto

mosquitto_sub -d -h 192.168.2.75 -p 1883 -t RMS1/+/STATUS -u 1BNFW2CF0BFA88801 -P 1BNFW2CF0BFA88801

* -d // 开启debug选项
* -h 192.168.2.75  // 说明所连接到的域名，默认是localhost
* -p 1883  // 连接的端口号，默认是1883.
* -t RMS1/+/STATUS  // 指定主题
* -u 1BNFW2CF0BFA88801  // 指定用户名用于代理认证。
* -P 1BNFW2CF0BFA88801 // 指定密码用于代理认证，使用此选项时必须有有效的用户名。
