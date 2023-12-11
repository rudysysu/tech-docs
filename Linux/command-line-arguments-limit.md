---
layout: docs
title: CommandLineArgumentsLimit
permalink: /linux/command-line-arguments-limit/
---

* toc
{: toc }

# show argument limit

~~~
$ xargs --show-limits
Your environment variables take up 2572 bytes
POSIX upper limit on argument length (this system): 2092532
POSIX smallest allowable upper limit on argument length (all systems): 4096
Maximum length of command we could actually use: 2089960
Size of command buffer we are actually using: 131072
~~~

# redhat

https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/6.8_Release_Notes/new_features_kernel.html

~~~
The /proc/pid/cmdline file length is now unlimited
The /proc/pid/cmdline file length limit for the ps command was previously hard-coded in the kernel to 4096 characters. 
This update makes sure the length of /proc/pid/cmdline is unlimited, 
which is especially useful for listing processes with long command line arguments. (BZ#1100069)
~~~

# stackoverflow

http://stackoverflow.com/questions/199130/how-do-i-increase-the-proc-pid-cmdline-4096-byte-limit

~~~
You can't change this dynamically, the limit is hard-coded in the kernel to PAGE_SIZE in fs/proc/base.c:
 274        int res = 0;
 275        unsigned int len;
 276        struct mm_struct *mm = get_task_mm(task);
 277        if (!mm)
 278                goto out;
 279        if (!mm->arg_end)
 280                goto out_mm;    /* Shh! No looking before we're done */
 281
 282        len = mm->arg_end - mm->arg_start;
 283 
 284        if (len > PAGE_SIZE)
 285                len = PAGE_SIZE;
 286 
 287        res = access_process_vm(task, mm->arg_start, buffer, len, 0);
~~~

# query linux version

~~~
cat /etc/issue
~~~
