# Usage
- 查看每个CPU信息： 按1
- 查看进程详情： 按c
- %st： 物理机虚拟了多个虚拟机，于是虚拟机之间互相抢cpu资源。 st指被其他虚拟机“偷取”的cpu资源比例。
- top -H -p 1234 // 查看子进程的资源占用情况
- TIME+: minute:second.second/100, such as 3:42.27
- Delete Process: press k -> input pid -> input level

# Example
	Tasks: 202 total,   2 running, 200 sleeping,   0 stopped,   0 zombie
	Cpu(s): 12.7%us,  0.0%sy,  0.0%ni, 87.3%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
	Mem:  32877676k total,  6275284k used, 26602392k free,   155032k buffers
	Swap:  4194300k total,        0k used,  4194300k free,   989008k cached

	  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
	 4494 reactor   20   0 8204m 3.8g  15m S 101.7 12.2   3:42.27 java
	   38 root      20   0     0    0    0 S  0.3  0.0   0:06.18 events/3
	 4473 reactor   20   0 9932m  85m  14m S  0.3  0.3   0:00.77 java
	20318 reactor   20   0 3673m 341m  12m S  0.3  1.1   1:29.99 java
		1 root      20   0 19232 1496 1224 S  0.0  0.0   0:01.33 init

# Cpu(s)
## 原始数据来自于/proc/stat
	[(integration)eyogdig@kafka-1 ~]$ cat /proc/stat
		 User time    Nice time    System time    Idle time    Waiting time    Hard Irq time    SoftIRQ time    Steal time    ???    ???    
	cpu  149734027    5006         46281356       1927754041   14015733        0                14963694        0             0      0
## man top
	%us: user   : time running un-niced user processes
	%sy: system : time running kernel processes
	%ni: nice   : time running niced user processes
	%id: idle   : time spent in the kernel idle handler 
	%wa: IO-wait: time waiting for I/O completion
	%hi         : time spent servicing hardware interrupts
	%si         : time spent servicing software interrupts 
	%st         : time stolen from this vm by the hypervisor

# Soft/Hard Irq
- 系统调用：用户进程需要通过操作系统提供的接口才能操作各种硬件资源，这些接口就是系统调用。（通过系统调用，用户进程才可以访问内核）
- 中断就是一个硬件或软件请求，要求CPU暂停当前的工作，去处理更重要的事情。比如，在x86机器上可以通过int指令进行软件中断，而在磁盘完成读写操作后会向CPU发起硬件中断。
- 硬中断：外围硬件发给CPU或者内存的异步信号就称之为硬中断
- 软中断：由软件系统本身发给操作系统内核的中断信号，称之为软中断。通常是由硬中断处理程序或进程调度程序对操作系统内核的中断，也就是我们常说的系统调用(System Call)

# References
- https://zhuanlan.zhihu.com/p/36995443
- https://blog.csdn.net/gatieme/article/details/50779184
- http://www.simlinux.com/2017/02/28/net-softirq.html