# Jmap

## Command
jmap -F -histo 6905

## Example
~~~
[cloud-user@ip-192-168-1-236 ~]$ sudo /usr/java/jdk1.7.0_101/bin/jmap -F -histo 7168
Attaching to process ID 7168, please wait...
Debugger attached successfully.
Server compiler detected.
JVM version is 24.101-b14
Iterating over heap. This may take a while...
Object Histogram:

num       #instances    #bytes  Class description
--------------------------------------------------------------------------
1:              103106  16176040        * ConstMethodKlass
2:              103106  13209904        * MethodKlass
3:              11920   12494080        * ConstantPoolKlass
4:              11920   9637712 * InstanceKlassKlass
5:              10220   7210944 * ConstantPoolCacheKlass
6:              23968   2223848 byte[]
7:              16158   1097344 short[]
8:              13176   1057160 char[]
~~~
