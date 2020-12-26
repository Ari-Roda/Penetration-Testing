once we know what hosts are alive and what OS's they have we can start looking for their running services and versions. This is done usually with port scanner programs. Its always possible that there is a security device like a /ids/ips between you and the target. Port scanners can be used to help find out and bypass this.

In the case of TCP, if a port is closed and you send a SYN packet to it it will return a RST+ACK (reset + acknowledgment). For successful cases you do a normal 3 way handshake and then the attacker sends RST+ACK to close connection. This is noisy because these connections get recorded in logs. TCP SYN scans were made to be more stealthy it doesnt complete the connection with the final ACK. It uses the response from the target to see if its up based on if it gives a RST+ACK or SYN+ACK and then doesnt send an ACK but instead sends a RST packet to stop full connection from happening and hence logging.


-sT TCP connect scan, full 3 way handshake scan that gets logged
-sS SYN scan : doesnt complete 3 way handshake so no logging
-sV version detection scan : get service versions running on ports. if the service doesnt send a banner on its own it sends probes to find out what the service running is. noisy
-p <ports> specify port to scan. -p- for all

in cases were a host is trying to hide and not responding to pings, we cant try to identify alive hosts in another way. there are certain ports that are almost always open if the host is up (22,445,80,443) can be used as indicators of a live host.
therefore you can force scanning on all hosts with -Pn but only check those ports.

-Pn forces scan on a server that doesnt respond to a ping.

To detect if some security device is in between you and the target, first pay attention to incomplete nmap results. for example an -sV shouldnt have a problem fingerprinting a http service in an open network. If it has parts missing like the version or even if a service type is not recognized (when it returns tcpwrapped or filtered) its an indication that something is blocking connectivity. --reason can be used to show an explanation of why a port is marked open or closed.

masscan is like nmap but faster and less accurate so you might want to use this for initial host discovery and then nmap afterwards for service discovery.

make -j


./masscan --regress

./masscan -p22,80,443,53,3389,8080,445 -Pn --rate=800 --banners ip-range -e tap1 --router-ip <ip>

change . conf file to ouput to file

##########################SSH OPEN PORTS########################################################

connect to ssh to see if the banner has any info which may help
