## Install
```bash
yum provides */iostat
yum install sysstat
```

## usage
iostat -xm 2 6
- -d     Display the device utilization report.
- -x     Display extended statistics.
- -k     Display statistics in kilobytes per second.
- -m     Display statistics in megabytes per second.
- 2 6    Display six reports at two second intervals for all devices.


## desc
- tps    每秒I/O数（即IOPS。磁盘连续读和连续写之和）
- Blk_read/s    每秒从设备读取的数据大小，单位是block/s（块每秒）
- Blk_wrtn/s    每秒写入设备的数量，单位是block/s
- Blk_read    从磁盘读出的块的总数
- Blk_wrtn    写入磁盘的块的总数
- kB_read/s    每秒从磁盘读取数据大小，单位KB/s
- kB_wrtn/s    每秒写入磁盘的数据的大小，单位KB/s
- kB_read      从磁盘读出的数据总数，单位KB
- kB_wrtn      写入磁盘的的数据总数，单位KB
- rrqm/s    每秒合并到设备的读取请求数
- wrqm/s    每秒合并到设备的写请求数
- r/s    每秒向磁盘发起的读操作数。
- w/s    每秒向磁盘发起的写操作数。
- rsec/s    每秒从设备读取的扇区数量。
- wsec/s    每秒向设备写入的扇区数量。
- avgrq-sz    I/O 请求的平均大小，以扇区为单位
- avgqu-sz    向设备发起的I/O 请求队列的的平均队列长度 // 这个有bug，应该要再除以10
- await    I/O 请求的平均等待时间，单位为毫秒。这个时间包括请求队列（这个概念很重要）消耗的时间和为每个请求服务的时间
- svctm    I/O 请求的平均服务时间，单位为毫秒（这个数据不可信！）
- %util    处理 I/O 请求所占用的时间的百分比，即设备利用率。I/O请求期间CPU时间的百分比（即设备的带宽利用率）。当这个值接近100%时，表示磁盘I/O已经饱和

await 的参数也要多和 svctm 来参考。差的过高就一定有 IO 的问题。

## example
```
[cloud-user@es-gis-1(MS) ~]$  iostat -xm 2
CEE_es-gis-1(192.168.34.167)
avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           4.39    0.00    3.76   25.81    0.13   65.91

Device:         rrqm/s   wrqm/s     r/s     w/s    rMB/s    wMB/s avgrq-sz avgqu-sz   await  svctm  %util
vda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
scd0              0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
vdb               0.00    54.50   19.50   30.00     6.24     0.31   270.87     2.85   86.22  19.41  96.10

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.75    0.00    1.38   24.19    0.00   72.68

Device:         rrqm/s   wrqm/s     r/s     w/s    rMB/s    wMB/s avgrq-sz avgqu-sz   await  svctm  %util
vda               0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
scd0              0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
vdb               0.00   272.00    8.00  123.50     2.79     1.51    66.98     3.33   26.03   7.54  99.15

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           4.89    0.00    3.39   28.11    0.13   63.49

Device:         rrqm/s   wrqm/s     r/s     w/s    rMB/s    wMB/s avgrq-sz avgqu-sz   await  svctm  %util
vda               0.00     0.50    0.00    1.00     0.00     0.01    12.00     0.00    0.50   0.50   0.05
scd0              0.00     0.00    0.00    0.00     0.00     0.00     0.00     0.00    0.00   0.00   0.00
vdb               0.00   172.00   15.00  116.50     1.89     0.88    43.07     1.47   11.72   7.48  98.30
```
