fastnetmon
=/=========

FastNetMon - High Performance Network Load Analyzer with PCAP/ULOG2 support

Install

```bash
   # Debian
   apt-get install -y git libpcap-dev g++ gcc libboost-all-dev
   # CentOS
   yum install -y git libpcap-devel gcc-c++ boost-devel boost

   # for traffic counting
   apt-get install -y libhiredis-dev

   git clone https://github.com/FastVPSEestiOu/fastnetmon.git
   cd fastnetmon
```

Select backend, we use ULOG2 as default, if you need PCAP u must change variable ENGINE in build.sh to PCAP

Compile it:
```bash
./build.sh
```

Start it:
```bash
./fastnetmon
```
Server configuration for PCAP:
 no configuration needed

Server configuration for ULOG2:
```bash
iptables -A FORWARD -i br0 -j ULOG --ulog-nlgroup 1 --ulog-cprange 32 --ulog-qthreshold 45
```

If you use PCAP, u can set monitored interface as command line parameter (u can set 'any' as inerface name but it work not so fine):
```bash
./fastnetmon br0
``` 

Example program screen:
```bash
Below you can see all clients with more than 2000 pps

Incoming Traffic    66167 pps 88 mbps
xx.yy.zz.15         3053  pps 0  Mbps
xx.yy.zz.248        2948  pps 0  Mbps
xx.yy.zz.192        2643  pps 0  Mbps

Outgoing traffic    91676 pps 728 mbps
xx.yy.zz.15         4471  pps 40  Mbps
xx.yy.zz.248        4468  pps 40  Mbps
xx.yy.zz.192        3905  pps 32  Mbps
xx.yy.zz.157        2923  pps 24  Mbps
xx.yy.zz.169        2809  pps 24  Mbps
xx.yy.zz            2380  pps 24  Mbps
xx.yy.zz            2105  pps 16  Mbps

Internal traffic    1 pps

Other traffic       25 pps

ULOG buffer errors: 2 (0%)
ULOG packets received: 19647
```

Author: Pavel Odintsov pavel.odintsov at gmail.com
