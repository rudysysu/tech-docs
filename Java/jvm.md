# Jvm

## Parameters
- -Xms10g
- -Xmx10g
- -XX:+PerfDisableSharedMem
  - This option helps sometimes to reduce JVM safepoint pauses, but it also makes JVM invisible to jps and jstat.

## Why does the JVM consume less memory than -Xms specified?
- example
```
PID USER      PR  NI  VIRT  RES       SHR S %CPU %MEM    TIME+  COMMAND
 4067 brian     20   0 5316m **262m** 7496 S    0  3.3   0:00.30 java -**Xms4096m** -Xmx4096m Test
 4066 brian     20   0 3182m **256m** 7496 S    0  3.3   0:00.30 java -**Xms2048m** -Xmx2048m Test
 4065 brian     20   0 2114m **252m** 7492 S    0  3.2   0:00.30 java -**Xms1024m** -Xmx1024m Test
 4064 brian     20   0 1314m  **76m** 7584 S    0  1.0   0:00.20 java -**Xms256m** -Xmx256m Test
 4063 brian     20   0 1180m  **51m** 7608 S    0  0.7   0:00.21 java -**Xms128m** -Xmx128m Test
```
- Answer
  - Xms option is used for JVM min-heap size definition
  - top shows the real memory(VIRT/RES/SHR) process used
```
use your example -Xms10g -Xmx10g, when jvm start, it will ask op-system allocation 10g memory which will be used for heap. And op-system will try to allocate the memory for the JVM (show as VIRT), but system did not promise u it will allocate physical memory, it maybe swap ;)
 
But u will find the VIRT is still not 10g, that reason is 10g is for heap size, a JVM include much more the heap, for example, stack, permgen(hotspot JDK8, openJDK seems has no permgen, fix me if i am wrong), native stack, code, files etc.

And RES is for real physical memory used, it includes new objects, method etc, still not only the heap too.
```
