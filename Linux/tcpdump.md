# tcpdump

## installation
yum install tcpdump

## parameter
- dst 127.0.0.1 and port 12345
- -i any // Listen on interface.
- -X // print the data of each packet in hex and ASCII.

## Example
- sudo tcpdump -i any dst 192.168.4.43 and dst port 12345 -X

## Reference
- https://en.wikipedia.org/wiki/Transmission_Control_Protocol
- https://danielmiessler.com/study/tcpdump/#gs.mnLLCXo

```
598  tcpdump -s 65535 -i any tcp and net 192.168.2.202/32 -w /tmp/test.pcap
599  tcpdump -s 65535 -i any tcp and net 192.168.2.202/32 -X
```

sudo nohup tcpdump -i any host 192.168.4.43 and port 12345 -X
sudo nohup tcpdump -i any host 192.168.4.43 and port 12345 -w ./device.pcap


sudo nohup tcpdump -i any host 192.168.4.43 and  port 12345 -w device.pcap &


Flags are some combination  of  S  (SYN),  F(FIN), P (PUSH), R (RST), U (URG), W (ECN CWR), E (ECN-Echo) or `.` (ACK), or `none` if no flags are set. 


sudo tcpdump -i any port 1883 -X

sudo tcpdump -i any port 1883 -w ~/rudy.pcap

tcp.port == 59442 and  mqtt

```
09:37:06.461130 IP ip-192-168-8-12.ap-northeast-1.compute.internal.53162 > ip-192-168-4-43.ap-northeast-1.compute.internal.italk: Flags [S], seq 4022686450, win 26883, options [mss 8961,sackOK,TS val 18025995 ecr 0,nop,wscale 8], length 0
        0x0000:  4500 003c 5cf9 4000 ff06 913a c0a8 080c  E..<\.@....:....
        0x0010:  c0a8 042b cfaa 3039 efc5 52f2 0000 0000  ...+..09..R.....
        0x0020:  a002 6903 e26c 0000 0204 2301 0402 080a  ..i..l....#.....
        0x0030:  0113 0e0b 0000 0000 0103 0308            ............
09:37:06.461157 IP ip-192-168-4-43.ap-northeast-1.compute.internal.italk > ip-192-168-8-12.ap-northeast-1.compute.internal.53162: Flags [S.], seq 3075921273, ack 4022686451, win 17898, options [mss 8961,sackOK,TS val 797215772 ecr 18025995,nop,wscale 7], length 0
        0x0000:  4500 003c 0000 4000 4006 ad34 c0a8 042b  E..<..@.@..4...+
        0x0010:  c0a8 080c 3039 cfaa b756 d579 efc5 52f3  ....09...V.y..R.
        0x0020:  a012 45ea bd04 0000 0204 2301 0402 080a  ..E.......#.....
        0x0030:  2f84 8c1c 0113 0e0b 0103 0307            /...........
09:37:06.461493 IP ip-192-168-8-12.ap-northeast-1.compute.internal.53162 > ip-192-168-4-43.ap-northeast-1.compute.internal.italk: Flags [.], ack 1, win 106, options [nop,nop,TS val 18025995 ecr 797215772], length 0
        0x0000:  4500 0034 5cfa 4000 ff06 9141 c0a8 080c  E..4\.@....A....
        0x0010:  c0a8 042b cfaa 3039 efc5 52f3 b756 d57a  ...+..09..R..V.z
        0x0020:  8010 006a 4e9e 0000 0101 080a 0113 0e0b  ...jN...........
        0x0030:  2f84 8c1c       


4500 003c => 4(ipv4); 5(head length 5*4=20bytes); 003c(all length 60bytes)
5cf9 4000 
ff06 913a 
c0a8 080c => source address(192.168.8.12)
c0a8 042b => destination address(192.168.4.43)

cfaa 3039 => cfaa(source port 53162); 3039(source port 12345); 
efc5 52f2 
0000 0000
a002 6903 
e26c 0000
 
0204 2301 
0402 080a
0113 0e0b 
0000 0000 
0103 0308          




4500 0034 
5cfa 4000 
ff06 9141 
c0a8 080c
c0a8 042b 

cfaa 3039 
efc5 52f3 => 4022686451
b756 d57a => 3075921274
8010 006a
4e9e 0000 
0101 080a 
0113 0e0b
2f84 8c1c       

```
