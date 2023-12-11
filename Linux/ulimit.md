# Summary

get and set user limits.

# Command

ulimit


## 修改配置
```
vim /etc/security/limits.conf
elasticsearch - nofile 65536
```

# 鳥哥的 Linux 私房菜

~~~
[dmtsai@study ~]$ ulimit [-SHacdfltu] [配額]
選項與參數：
-H  ：hard limit ，嚴格的設定，必定不能超過這個設定的數值；
-S  ：soft limit ，警告的設定，可以超過這個設定值，但是若超過則有警告訊息。
      在設定上，通常 soft 會比 hard 小，舉例來說，soft 可設定為 80 而 hard 
      設定為 100，那麼你可以使用到 90 (因為沒有超過 100)，但介於 80~100 之間時，
      系統會有警告訊息通知你！
-a  ：後面不接任何選項與參數，可列出所有的限制額度；
-c  ：當某些程式發生錯誤時，系統可能會將該程式在記憶體中的資訊寫成檔案(除錯用)，
      這種檔案就被稱為核心檔案(core file)。此為限制每個核心檔案的最大容量。
-f  ：此 shell 可以建立的最大檔案容量(一般可能設定為 2GB)單位為 Kbytes
-d  ：程序可使用的最大斷裂記憶體(segment)容量；
-l  ：可用於鎖定 (lock) 的記憶體量
-t  ：可使用的最大 CPU 時間 (單位為秒)
-u  ：單一使用者可以使用的最大程序(process)數量。

範例一：列出你目前身份(假設為一般帳號)的所有限制資料數值
[dmtsai@study ~]$ ulimit -a
core file size          (blocks, -c) 0          <==只要是 0 就代表沒限制
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited  <==可建立的單一檔案的大小
pending signals                 (-i) 4903
max locked memory       (kbytes, -l) 64
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024       <==同時可開啟的檔案數量
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 4096
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited

範例二：限制使用者僅能建立 10MBytes 以下的容量的檔案
[dmtsai@study ~]$ ulimit -f 10240
[dmtsai@study ~]$ ulimit -a | grep 'file size'
core file size          (blocks, -c) 0
file size               (blocks, -f) 10240 <==最大量為10240Kbyes，相當10Mbytes

[dmtsai@study ~]$ dd if=/dev/zero of=123 bs=1M count=20
File size limit exceeded (core dumped) <==嘗試建立 20MB 的檔案，結果失敗了！

[dmtsai@study ~]$ rm 123  <==趕快將這個檔案刪除囉！同時你得要登出再次的登入才能解開 10M 的限制
~~~

# DDI

~~~
DDI在之前openstack环境安装create image时就参照DDI的安装Guide批量作系统参数调整的，
我检查其中的任一台机器文件 /etc/security/limits.conf 末尾如增加如下配置的: 
- hard nproc 32768
- hard nofile 65536
- soft nproc 8192
- soft nofile 8192
~~~

# ECE 

~~~
ECE 的话安装的时候就会安装一个调优的描述档案（俗称加速包）到系统里面，所以没什么要调的了。
DDI 的 Installation Guide 里面有最基本的，附在下面：
5.2   Operating System Settings
Before starting the installation, configure the following settings for all target operating system. 
Note:  
DDI components cannot be started successfully if the values are too low.

Configuring Number of Open Processes
For maximum performance, it is recommended that the soft limit for the number of open processes is set to at least 8192.
To set the maximum number of open processes to 8192, do the following:
1.	Use ulimit -u 8192 to set the value.
2.	Use ulimit -u to verify that the value has been correctly set.
This value cannot be greater than the hardware limit for the system. Check the hardware limit and modify it if needed.
Note:  
The following changes must be performed as root user.

Use the following command to check the hard limit:
ulimit -H –u
Use the following commands to set the hard limit:
Edit /etc/security/limits.conf
* hard nproc 32768
Setting the Numbers of Open Files
For maximum performance, it is recommended that the soft limit for the number of open files is set to at least 8192. 
Note:  
Ensure that this value is set before installing DDI components.

To set the logon environment limit, do the following:
1.	Use ulimit -n 8192 to set the value.
2.	Use ulimit -n to verify that the value has been correctly set.
This value cannot be greater than the hard limit for the system. Check the hard limit and modify if needed.
Note:  
The following change must be performed as root user. 

Use the following command to check the hard limit:
ulimit -H –u
Use the following commands to modify the hard limit:
Linux
Edit /etc/security/limits.conf
* hard nofile 65536
~~~
