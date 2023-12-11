sar（System Activity Reporter系统活动情况报告）是目前 Linux 上最为全面的系统性能分析工具之一，可以从多方面对系统的活动进行报告，包括：文件的读写情况、 系统调用的使用情况、磁盘I/O、CPU效率、内存使用状况、进程活动及IPC有关的活动等。本文主要以CentOS 6.3 x64系统为例，介绍sar命令。

## 安装sar工具
apt-get install sysstat

## sar命令常用格式
`sar [options] [-A] [-o file] t [n]`

其中：
- t为采样间隔，n为采样次数，默认值是1；
- -o file表示将命令结果以二进制格式存放在文件中，file 是文件名。
- options 为命令行选项，sar命令常用选项如下：
    - -A：所有报告的总和
    - -u：输出CPU使用情况的统计信息
    - -v：输出inode、文件和其他内核表的统计信息
    - -d：输出每一个块设备的活动信息
    - -r：输出内存和交换空间的统计信息
    - -b：显示I/O和传送速率的统计信息
    - -a：文件读写情况
    - -c：输出进程统计信息，每秒创建的进程数
    - -R：输出内存页面的统计信息
    - -y：终端设备活动情况
    - -w：输出系统交换活动信息

内存输出项说明：
- kbmemfree：这个值和free命令中的free值基本一致,所以它不包括buffer和cache的空间.
- kbmemused：这个值和free命令中的used值基本一致,所以它包括buffer和cache的空间.
- %memused：这个值是kbmemused和内存总量(不包括swap)的一个百分比.
- kbbuffers和kbcached：这两个值就是free命令中的buffer和cache.
- kbcommit：保证当前系统所需要的内存,即为了确保不溢出而需要的内存(RAM+swap).
- %commit：这个值是kbcommit与内存总量(包括swap)的一个百分比.
- kbactive：活跃内存的大小(内存最近被使用过，并且不会被回收) 
- kbinact：不活跃内存大小(最近未被使用的内存，很符合回收策略的内存)

## References
- [linux sar 命令详解](assets/linux-sar/linux sar 命令详解 - 阳台 - 博客园.mhtml)
- https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/sar.html