# yum

```
yum updateinfo
yum provides */netstat
yum list installed
yum info docker
```

## Install Epel Repo
ansible all -i ansible, -m yum -a 'name=epel-release state=present' --ssh-common-args='-o StrictHostKeyChecking=no'


## Install Local Repo
- yum install createrepo 
- createrepo -pdo /data/RPMs/ /data/RPMs/
- sync repos to local

```
yum install rsync
rsync -avz --progress --no-motd rsync://mirrors.ustc.edu.cn/centos/7/os/x86_64/ /data/RPMs/centos_7_os_x86_64/
rsync -avz --progress --no-motd rsync://mirrors.ustc.edu.cn/centos/7/updates/x86_64/ /data/RPMs/centos_7_updates_x86_64/
rsync -avz --progress --no-motd rsync://mirrors.ustc.edu.cn/centos/7/extras/x86_64/ /data/RPMs/centos_7_extras_x86_64/
```

- 开http服务指向/data/RPMs/，如nginx

```
[root@localhost RPMs]# cat /etc/nginx/conf.d/RPMs.conf 
server {
    listen      81;
    server_name ansible.dy.com;

    access_log /var/log/nginx/ansible.dy.com.access.log  main;
    error_log  /var/log/nginx/ansible.dy.com.error.log  debug;

    index  index.html;

    root /data/RPMs/;
    autoindex on;
}

注意selinux要关掉，否则nginx可能无法访问目录。
```

- Config Local Repo

```
[root@k8s-2 ~]# cat /etc/yum.repos.d/local.repo 
[local]
name=Local software
baseurl="http://ansible.dy.com:81"
gpgcheck=0
```

## References
- [CentOS7下的软件安装方法及策略详解](https://www.jb51.net/os/RedHat/529749.html)
- [搭建本地yum源服务器](https://www.cnblogs.com/weijing24/p/5638725.html)
- [在linux下如何使用yum查看安装了哪些软件包](https://blog.csdn.net/wenwenxiong/article/details/51785221)