# fuser
- identify processes using files or sockets

## usage
- fuser ${pid} -uv
- example
```
root@ubuntu64:/var/log/carbon# fuser console.log -uv
                     USER        PID ACCESS COMMAND
/var/log/carbon/console.log:
                     _graphite   1141 F.... (_graphite)carbon-cache
```

## help
```
root@ubuntu64:/var/log/carbon# fuser
No process specification given
Usage: fuser [-fMuvw] [-a|-s] [-4|-6] [-c|-m|-n SPACE] [-k [-i] [-SIGNAL]] NAME...
       fuser -l
       fuser -V
Show which processes use the named files, sockets, or filesystems.

  -a,--all              display unused files too
  -i,--interactive      ask before killing (ignored without -k)
  -k,--kill             kill processes accessing the named file
  -l,--list-signals     list available signal names
  -m,--mount            show all processes using the named filesystems or block device
  -M,--ismountpoint     fulfill request only if NAME is a mount point
  -n,--namespace SPACE  search in this name space (file, udp, or tcp)
  -s,--silent           silent operation
  -SIGNAL               send this signal instead of SIGKILL
  -u,--user             display user IDs
  -v,--verbose          verbose output
  -w,--writeonly        kill only processes with write access
  -V,--version          display version information
  -4,--ipv4             search IPv4 sockets only
  -6,--ipv6             search IPv6 sockets only
  -                     reset options

  udp/tcp names: [local_port][,[rmt_host][,[rmt_port]]]
```
