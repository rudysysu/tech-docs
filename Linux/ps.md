# SIMPLE PROCESS SELECTION

~~~
ax: all processes;
a: all processes with a terminal
x: all processes owned by you
r: all processes with running.
~~~

# PROCESS SELECTION BY LIST

~~~
-u: Select by effective user ID (EUID) or name.
-p: Select by process ID. such as: ps -p 123,456,789
--ppid: Select by parent process ID.
-t: Select by terminal.
~~~

# OUTPUT FORMAT CONTROL

~~~
u: Display user-oriented format.
l: Display BSD long format.
j: BSD job control format.
~~~

# OUTPUT MODIFIERS

~~~
ww: Wide output.
e: Show the environment after the command.
c: Show only the command name, no args
--headers: Repeat headers.
--no-headers: No header.
--sort: sorting.[+|-]key[,[+|-]key[,...]], such as: ps ax --sort user,-pid
--forest: ASCII art process hierarchy (forest).
~~~

# THREAD DISPLAY

~~~
H: Show threads as if they were processes.
m: Show threads after processes.
~~~

# PROCESS STATE CODES

~~~
the state of a process:
    D    uninterruptible sleep (usually IO)
    R    running or runnable (on run queue)
    S    interruptible sleep (waiting for an event to complete)
    T    stopped, either by a job control signal or because it is being traced
    W    paging (not valid since the 2.6.xx kernel)
    X    dead (should never be seen)
    Z    defunct ("zombie") process, terminated but not reaped by its parent
additional characters:
    <    high-priority (not nice to other users)
    N    low-priority (nice to other users)
    L    has pages locked into memory (for real-time and custom IO)
    s    is a session leader
    l    is multi-threaded (using CLONE_THREAD, like NPTL pthreads do)
    +    is in the foreground process group
~~~

# OUTPUT DESC

~~~
USER：进程所有者
PID：进程ID
%CPU：占用的CPU使用率
%MEM：占用的内存使用率
VSZ：占用的虚拟内存大小
RSS：占用的物理内存大小
TTY：终端编号
STAT：进程状态
START：进程启动时间
TIME：进程消耗CPU的时间
COMMAND：命令的名称和参数
~~~
