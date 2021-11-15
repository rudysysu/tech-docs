## 手动Mount
sudo mount -t cifs //192.168.1.1/t_drive /media/t_drive  -o rw,vers=1.0,username=admin,password=XXX

## 自动Mount
vim /etc/fstab

### 挂载本地磁盘
/dev/disk/by-uuid/70240EAD240E767E /media/rudy/SATA auto nosuid,nodev,nofail,x-gvfs-show 0 0

### 挂载SMB远程磁盘
//192.168.1.1/t_drive /media/t_drive cifs vers=1.0,username=admin,password=XXX 0 0  
这里的版本号很关键，如果配置为高版本（比如2.1和3.0），可能会报找不到目录。

### 立即挂载
mount -a

## 参考文献
https://blog.csdn.net/yanchaoccc/article/details/79558327
