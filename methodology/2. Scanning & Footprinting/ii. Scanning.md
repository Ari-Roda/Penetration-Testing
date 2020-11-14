1. 
Initial scanning can be done with scanning programs such as nmap, masscan or fping. the idea is to find out which hosts are up from an ip range to narrow down our next steps.

```fping -a -g <first ip last ip> or iprange/24``` : ping a range of ips to find out which ones are up. -a is show only live hosts and -g for ping sweep not normal ping
#when running fping on  a lan your are directly attached to with -a you will get warnings (ICMP host unreachable) about offline hosts so use 2>/dev/null
  
```nmap -sn <variious notations for ip range>``` : -sn no port scan, -iL to take input ip's from txt file. more host discovery options available 
  
This can be done in steps such as doing basic scan above first and then more scans of different complexity to allow for faster analysis if your time restricted. For example, queue up ping scan, port scan and service scan. This can also be done in one go which may take time to finish. Tools like autorecon can be used which do many scans of different complexity on an IP or group of IP's but it fully scans each host which is super inefficient.


```fping -a -g <first ip last ip> or iprange/24> 2>/dev/null```

```nmap -sn <ip range>```

```sudo nmap -sS -iL ips.txt```

```nmap -sV -iL ips.txt```

```sudo nmap -O --osscan-guess -iL ips.txt```

