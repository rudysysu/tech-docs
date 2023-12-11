

## 显示Centos启动命令详细信息
vim /etc/grub2.cfg
删除两处： rhgb quiet

"rhgb"表示"redhat graphics boot"

## Update host name
```
vi /etc/hostname
```

## install

```bash
yum updateinfo

yum provides */rz
yum install lrzsz

yum provides */netstat
yum install net-tools

yum install vim
yum install ansible
yum install zip unzip
```