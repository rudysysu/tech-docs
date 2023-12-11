# Sort

```
用于排序，如：
    cat /data/weblog/java/star.m.yy.com/star/star.log | grep 'PhotoCommentAction:225' | awk '{print $6}' | sort -n

-n：按数值排序
-r：逆序排序
-t：指定列分隔符
-k：指定排序的列，–key=POS1[,POS2] 指定一个或几个字段作为排序关键字，字段位置从posl开始，到pos2为止(包括post1但是不包括post2),如不指定pos2，则关键字为从posl到行尾。字段和字符的位置从0开始。FREEBSD是从1开始
-k 3,3nr -k 2,2n：先按第3列数值逆序排序，再按第2列数值顺序排序
```
