为什么需要cgroup
	对进程进行分组，并在分组的基础上对进程进行监控和资源控制管理等。
	
什么是cgroup
	cgroup技术就是把系统中的所有进程组织成一颗一颗独立的树，每棵树都包含系统的所有进程，树的每个节点是一个进程组，而每颗树又和一个或者多个subsystem关联，树的作用是将进程分组，而subsystem的作用就是对这些组进行操作。
	
耗CPU的例子：
	x=0
	while [ True ];do
		x=$x+1
	done;
	
限制CPU方法：
1. mkdir /sys/fs/cgroup/cpu/rudy // 这样就会创建一个子分组
2. cat /cgroup/cpu/cpu.cfs_period_us // 时间周期，默认为 100000，即百毫秒
3. echo 50000 > /sys/fs/cgroup/cpu/rudy/cpu.cfs_quota_us // 设置该子分组，在每时间周期内使用的时间是50000，即使用了50%的时间。
4. echo 7118 >> /sys/fs/cgroup/cpu/rudy/tasks // 把耗CPU的进程加入到这个子分组，这样该进程就只能占用50%的CPU时间。
	
	
参考文献：
[1] 入门的参考文献：https://segmentfault.com/a/1190000006917884
[2] 限制CPU占有率的例子：https://www.cnblogs.com/yanghuahui/p/3751826.html
[3] 较好解释cfs_quota_us/cfs_period_us的文档：http://xiezhenye.com/2013/10/%E7%94%A8-cgroups-%E7%AE%A1%E7%90%86-cpu-%E8%B5%84%E6%BA%90.html
[4] 官方文档（需要认真读下）：https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/7/html/resource_management_guide/