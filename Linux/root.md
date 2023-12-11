## 允许root登录
```
sudo –s 切换到root
passwd设置root密码
```

## 允许root远程登录
```
vi /etc/ssh/sshd_config
PermitRootLogin yes
service ssh restart
```
