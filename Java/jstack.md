# Jstack

## Command
~~~bash
jstack -F -m 31301
-m: display native
~~~

## Example
~~~
Deadlock Detection:

No deadlocks found.

----------------- 31303 -----------------
0x00007fa8d6cda63c      __pthread_cond_wait + 0xcc
0x00007fa8d5e899df      _ZN7Monitor5IWaitEP6Threadl + 0xef
0x00007fa8d5e8a02d      _ZN7Monitor4waitEblb + 0xed
0x00007fa8d60011c1      _ZN7Threads10destroy_vmEv + 0x51
0x00007fa8d5ce01f0      jni_DestroyJavaVM + 0xc0
0x00007fa8d6abd16d      JavaMain + 0x27d
----------------- 31304 -----------------
0x00007fa8d5f1a858      _ZN20ParCompactionManager21follow_marking_stacksEv + 0x188
0x00007fa8d5f01f49      _ZN16StealMarkingTask5do_itEP13GCTaskManagerj + 0x2c9
0x00007fa8d5bfd78f      _ZN12GCTaskThread3runEv + 0x12f
0x00007fa8d5ec8f08      _ZL10java_startP6Thread + 0x108
----------------- 31305 -----------------
0x00007fa8d65f12c7      __GI_sched_yield + 0x7
0x00007fa8d5f01ff2      _ZN16StealMarkingTask5do_itEP13GCTaskManagerj + 0x372
0x00007fa8d5bfd78f      _ZN12GCTaskThread3runEv + 0x12f
0x00007fa8d5ec8f08      _ZL10java_startP6Thread + 0x108
----------------- 31306 -----------------
0x00007fa8d5fd0d50      _ZN22ParallelTaskTerminator17offer_terminationEP20TerminatorTerminator + 0xd0
0x00007fa8d5f01ff2      _ZN16StealMarkingTask5do_itEP13GCTaskManagerj + 0x372
0x00007fa8d5bfd78f      _ZN12GCTaskThread3runEv + 0x12f
0x00007fa8d5ec8f08      _ZL10java_startP6Thread + 0x108
----------------- 31307 -----------------
0x00007fa8d5defca2              ????????
0x00007fa8d5f01ff2      _ZN16StealMarkingTask5do_itEP13GCTaskManagerj + 0x372
0x00007fa8d5bfd78f      _ZN12GCTaskThread3runEv + 0x12f
0x00007fa8d5ec8f08      _ZL10java_startP6Thread + 0x108
----------------- 31308 -----------------
0x00007fa8d5defca2              ????????
0x00007fa8d5f01ff2      _ZN16StealMarkingTask5do_itEP13GCTaskManagerj + 0x372
0x00007fa8d5bfd78f      _ZN12GCTaskThread3runEv + 0x12f
0x00007fa8d5ec8f08      _ZL10java_startP6Thread + 0x108
~~~
