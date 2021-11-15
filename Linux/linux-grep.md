## tail -f 多次grep过滤输出可能会出现的问题
```
对日志记录做多次grep过滤输出，格式如下：
tail -f log | grep xxx | grep yyy
发现grep失效，无法做正确输出。google研究了一下，原因如下：
管道 | 是全缓冲的，一般来说buffer_size为4096，有些是8192。不管具体值多少，只有buffer_size满了，才会看到输出。
在操作里  >>file 这个操作也是全缓冲的。调整如下
tail -f log | grep --line-buffer xxx | grep --line-buffer yyy
结果输出正常。
grep当带上了 --line-buffer 的时候，每输出一行，就刷新一次。
在unix里，块设备和普通文件，以及管道都是全缓冲的。
```