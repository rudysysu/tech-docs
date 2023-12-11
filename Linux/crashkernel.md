First, the below log not means exist an memory issue. This message will be printed while the OS is rebooted every time. 
Apr  1 13:49:44 post-ddi-1 kernel: Reserving 131MB of memory at 48MB for crashkernel (System RAM: 33792MB)

From the /var/log/messages-20190407, we do not see anything about the system shutdown process, such as “Stopping OpenSSH server daemon...”
Apr  1 13:42:01 post-ddi-1 audispd: node=post-ddi-1.novalocal type=CRED_ACQ msg=audit(1554111721.029:10712606): user pid=18017 uid=0 auid=500 ses=3144 msg='op=PAM:setcred acct="pg" exe="/bin/su" hostname=? addr=? terminal=? res=success'
Apr  1 13:42:01 post-ddi-1 audispd: node=post-ddi-1.novalocal type=CRED_DISP msg=audit(1554111721.034:10712607): user pid=Apr  1 13:49:44 post-ddi-1 kernel: imklog 5.8.10, log source = /proc/kmsg started.
// here do not have any shutdown related log
Apr  1 13:49:44 post-ddi-1 rsyslogd: [origin software="rsyslogd" swVersion="5.8.10" x-pid="1252" x-info="http://www.rsyslog.com"] start
Apr  1 13:49:44 post-ddi-1 kernel: Initializing cgroup subsys cpuset

From the /var/crash/, we do not see anything.
[cloud-user@post-ddi-1(MS) log]$ ls /var/crash/
[cloud-user@post-ddi-1(MS) log]$

So, I think this is because the OS do not have chance to do something before rebooting. Reason maybe: OS Bug, Power Off, Physical Restart.
